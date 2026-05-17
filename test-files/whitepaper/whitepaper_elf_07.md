---
title: Job scheduling mechanism
sidebar_label: Job scheduling mechanism
hide_title: true
id: whitepaper_elf_07
---

# Job scheduling mechanism

The Job Center scheduling mechanism is based on a directed acyclic graph (DAG), where each node represents a Follower task and each directed edge represents a dependency between tasks.

The task scheduling rules are as follows:

- Among all Follower tasks forming the DAG, a task with an in-degree of 0 is called a ready task, meaning it has no dependencies or all its dependencies have completed; it is ready to be executed.
- When the Leader submits tasks to Followers, it submits all ready tasks.
- When a Follower task completes, the Follower checks whether any downstream tasks that depend on it are now ready to execute and submits them to one or more Followers.
- The criterion for checking whether new tasks are ready: after removing the current Follower's task node, check whether any new ready task nodes have appeared.
- Each Follower task's database update operations must be atomic throughout the entire Job execution cycle, to ensure that multiple upstream tasks of the same Follower see a consistent state of their downstream task at the same moment, thereby guaranteeing correct execution order.
- A failed task node is not removed from the graph; instead, the Follower marks all tasks that directly or indirectly depend on it as failed.
- The last task to complete or fail is resubmitted to the Leader.

The following two examples illustrate how subtasks are scheduled in Job Center.

![](../assets/elf-white-paper/image3.png)

## Successful Job

As shown in the diagram above, the concurrent execution steps are as follows:

1. The Leader receives the tasks and builds the DAG. It determines that three tasks ①②③ that can be executed concurrently and submits them.
2. After ① completes, dependencies `a` and `b` are removed. However, ④ and ⑦ still have dependencies and cannot execute, so no new tasks are triggered.
3. After ② completes, dependencies `c`, `d`, `e`, and `f` are removed. ④⑤⑥ become ready tasks and are submitted by ②'s Follower.
4. After ③ completes, no new dependencies are removed. All currently ready tasks are still running, so no new tasks are triggered.
5. After ⑤ completes, dependency `i` is removed. However, ⑧ still depends on ⑥ and cannot be triggered, so no new tasks are triggered.
6. After ④ completes, dependencies `g` and `h` are removed. ⑦ becomes a ready task and is submitted by ④'s Follower. ⑨ still depends on ⑥, so no new tasks are triggered.
7. After ⑥ completes, dependencies `j` and `k` are removed. ⑧⑨ become ready tasks and are submitted by ⑥'s Follower.
8. After ⑧ completes, there are no more executable tasks.
9. After ⑨ completes, there are no more executable tasks.
10. After ⑦ completes, all tasks are done. A message is triggered and resubmitted to the Leader to finalize.
11. The Leader verifies all tasks succeeded, marks the Job as Done, and exits.

## Failed Job

As shown in the diagram above, the concurrent execution steps are as follows, with task ④ failing:

1. The Leader receives the tasks and builds the DAG. It determines that three tasks ①②③ that can be executed concurrently and submits them.
2. After ① completes, dependencies `a` and `b` are removed. However, ④ and ⑦ still have dependencies and cannot execute, so no new tasks are triggered.
3. After ② completes, dependencies `c`, `d`, `e`, and `f` are removed. ④⑤⑥ become ready tasks and are submitted by ②'s Follower.
4. After ③ completes, no new dependencies are removed. All currently ready tasks are still running, so no new tasks are triggered.
5. After ⑤ completes, dependency `i` is removed. However, ⑧ still depends on ⑥ and cannot be triggered, so no new tasks are triggered.
6. ④ fails; all downstream tasks related to ④, namely ⑦ and ⑨, are marked as failed.
7. After ⑥ completes, dependencies `j` and `k` are removed. ⑧⑨ would be ready tasks, but ⑨ is marked as failed, so only ⑧ is submitted.
8. After ⑧ completes, all tasks are done. A message is triggered and resubmitted to the Leader to finalize.
9. The Leader marks the Job as Failed and exits.

All graph updates must be atomic. When step 7 executes, the downstream tasks ⑦ and ⑨ related to ④ must already be in a failed state. Swapping the order of steps 6 and 7 does not produce a different result. If steps 6 and 7 complete simultaneously, Job Center periodically detects this situation and submits ready task ⑧.

## Node power failure causing Follower/Leader failure mid-execution

If any in-flight Follower is unable to execute due to a power failure or network interruption, a scheduled task triggered by the Scheduler checks the status of all subtasks of running Jobs, including each subtask's executor Handler (see [Job Recovery mechanism](#job-recovery-mechanism)), start time, and the timeout duration for submitted but unexecuted tasks. Any abnormal tasks are resubmitted, and the system waits for the final Follower to trigger the Leader to complete the Job. If execution is interrupted after all Followers have completed but before the result is submitted back to the Leader—due to a power failure or system crash—the Scheduler resubmits the task to the Leader for processing.

## Job Recovery mechanism

The Job Recovery mechanism is designed to ensure that any distributed task is always in either a "completed" or "failed" state, and never in an intermediate state. For example, failures caused by power, network, disk, or OS issues do not leave any task (such as creating a virtual machine or creating a disk) in an intermediate state that would lock the resource.

Job Recovery is implemented as a scheduled task that checks periodically. When the scheduled time arrives, Job Center Scheduler triggers a task and sends it to Job Center Worker to check whether any Jobs need recovery. The task sent to Job Center Worker is a cluster task with no specified node, so it works as long as at least one node in the cluster is healthy.

In addition, because Job Recovery tasks are cluster tasks, to prevent an accumulation of too many tasks of the same type due to delays or burst task volumes, the Job Queue feature is used to ensure only one cluster recovery task runs at a time.

The Job description contains the following information used for recovery determination:

- Handler

  Records the current handler of the Job or its subtask, identified by the temporary UUID assigned when each Job Center Worker starts.

- Creation time of Job and each subtask

  The creation time of the Job is the time it was submitted to the database; the creation time of a subtask is the time it was written to the database after Splitter analysis.

- Last modification time of Job and each subtask

- Completion time of Job and each subtask

  The completion time of a subtask is the time that the individual subtask is completed; the completion time of the Job is the time all tasks in the Job are completed.

Job Recovery rules:

- Check all running and non-running Jobs every minute.
- Each Job and its subtasks must record the assigned time, execution time, and Handler ID.
- If the Handler is no longer running, resubmit the Job or subtask to Job Center for processing.
- If the Handler has not been written for more than 5 minutes: if it is a Leader task, resubmit it; if it is a Follower task, submit the corresponding task to Job Center for processing. If the subtask targets a specific node but that node is unresponsive, mark the subtask as failed.
- If all subtasks of a Job have completed but the Job has not been marked as complete or failed for more than 1 minute, resubmit the Job to Job Center for processing.
- If duplicate task messages are sent to Job Center, it will not be resubmitted. When a task is marked as failed, clean up any waiting or incomplete messages.
- If a Job requiring resubmission is of the Scheduler type, it will not be resubmitted; instead mark the entire Job and all incomplete subtasks as Failed, to prevent a large number of scheduled tasks from continuously retrying.
