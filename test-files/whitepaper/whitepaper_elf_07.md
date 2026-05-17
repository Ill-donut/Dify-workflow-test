---
title: Job Scheduling Mechanism
sidebar_label: Job Scheduling Mechanism
hide_title: true
id: whitepaper_elf_07
---

# Job Scheduling Mechanism

The scheduling mechanism of Job Center is based on a directed acyclic graph, and each node in the graph is a Follower task. The straight lines with arrows indicate the dependency relationships between tasks.

Task scheduling follows these principles:

- In the directed acyclic graph formed by all Follower tasks, nodes with in-degree 0 are called ready tasks, indicating that the task has no dependent tasks or its dependent tasks have already been completed, and the task is ready and waiting to be executed;

- When the Leader submits tasks to the Followers, it submits all ready tasks;

- When a Follower task completes, the Follower needs to check whether downstream tasks that depend on this task have any executable tasks and submit them to one or more next Followers;

- The criterion for a Follower to check whether there are new tasks that can be executed is: after deleting the current Follower's task node, whether new ready task nodes are generated;

- The database update operation for each Follower task must ensure atomicity throughout the entire Job execution cycle, to ensure that multiple upstream tasks of the Follower task see a consistent downstream task state at the same time, thereby ensuring that tasks are executed correctly according to the workflow;

- Failed tasks will not have their nodes deleted, and this Follower will mark all tasks that directly or indirectly depend on this task as failed;

- The last completed or failed Follower submits back to the Leader again.

Below are two simple examples to illustrate how subtasks are scheduled in Job Center.

![](../assets/elf-white-paper/image3.png)

## Normal Successful Job

As shown in the figure above, the concurrent execution steps are summarized as follows:

1. The Leader receives the task and builds the DAG, determines that there are three tasks that can be executed concurrently, namely ① ② ③, and submits the tasks;

2. After ① finishes, dependencies a and b disappear, but ④ and ⑦ still have dependencies and cannot be executed, so it exits;

3. After ② finishes, dependencies c, d, e, and f disappear. ④ ⑤ ⑥ can be executed as ready tasks, so the tasks ④ ⑤ ⑥ are triggered and sent by the Follower of ②;

4. After ③ finishes, it disappears without generating dependencies. All executable ready tasks are currently still running, so it exits;

5. After ⑤ finishes, dependency i disappears, but ⑧ still depends on ⑥, so the task cannot be triggered, and it exits;

6. After ④ finishes, dependencies g and h disappear, ⑦ becomes a ready task and is triggered and sent by the Follower of ④. ⑨ still depends on ⑥, so it exits;

7. After ⑥ finishes, dependencies j and k disappear, ⑧ and ⑨ become ready tasks, and are triggered and sent by the Follower of ⑥;

8. After ⑧ finishes, there are no executable tasks, so it exits;

9. After ⑨ finishes, there are no executable tasks, so it exits;

10. After ⑦ finishes, all tasks are complete, and a message is triggered and resent to the Leader for final summary and completion;

11. The Leader checks that all tasks succeeded, marks the Job as Done, and exits;

## Job Fails Midway

As shown in the figure above, the concurrent execution steps are summarized as follows, with task ④ failing during execution:

1. The Leader receives the task and builds the DAG, determines that there are three tasks that can be executed concurrently, namely ① ② ③, and submits the tasks;

2. After ① finishes, dependencies a and b disappear, but ④ and ⑦ still have dependencies and cannot be executed, so it exits;

3. After ② finishes, dependencies c, d, e, and f disappear. ④ ⑤ ⑥ can be executed as ready tasks, so the tasks ④ ⑤ ⑥ are triggered and sent by the Follower of ②;

4. After ③ finishes, it disappears without generating dependencies. All executable ready tasks are currently still running, so it exits;

5. After ⑤ finishes, dependency i disappears, but ⑧ still depends on ⑥, so the task cannot be triggered, and it exits;

6. Task ④ fails. Mark all downstream tasks related to ④ as failed, that is, ⑦ ⑨, and exit;

7. After ⑥ finishes, dependencies j and k disappear. ⑧ and ⑨ are ready tasks, but ⑨ has been marked as failed, so only task ⑧ is submitted;

8. After ⑧ finishes, it is checked that all tasks have been completed, and a message is triggered and resent to the Leader for final summary and completion;

9. The Leader marks the Job as Failed and exits;

All graph updates must be atomic operations. When step 7 is executed, the downstream tasks ⑦ and ⑨ related to ④ must both be in the failed state. In the above tasks, swapping steps 6 and 7 will not produce a different result. If steps 6 and 7 finish at the same time, Job Center will periodically detect this situation and submit the ready task ⑧.

## Follower/Leader Failure Caused by Power Loss of a Node During Execution

If any Follower during execution cannot continue due to power loss or network interruption, the scheduled task triggered by the Scheduler will check the subtasks' states for all running Jobs, including the subtask executor Handler ([see Job Recovery Mechanism](#job-recovery-mechanism)), start time, and the timeout for tasks that were submitted but not executed. Abnormal tasks will be resubmitted, and then it waits for the final Follower to trigger the Leader to complete the Job. If execution is interrupted because of power loss or a crash when all Followers have finished and there was no time to submit back to the Leader, then the Scheduler resubmits the task to the Leader for processing.

## Job Recovery Mechanism

The purpose of Job Recovery is to handle distributed tasks in either the "completed" or "failed" state at any time, without an intermediate state. For example, failures in power, network, disk, operating system, and so on will not leave any task, such as creating a virtual machine or creating a disk, in an intermediate state that locks resources.

Job Recovery is implemented through a periodic scheduled task. When the scheduled time is reached, Job Center Scheduler will trigger a task and send it to Job Center Worker to check whether there are Jobs that need recovery. The task sent to Job Center Worker is a cluster task and does not specify a node, so as long as at least one node in the cluster is normal, it can work properly.

In addition, because the Job Recovery task is a cluster task, to prevent too many tasks of the same type from accumulating due to delays or a sudden burst of tasks, the characteristics of the Job Queue are used to control that only one cluster recovery task can exist at the same time.

The Job description contains the following information used for recovery decisions:

- Handler

  Used to record the current handler of a Job or a subtask under the Job. The content is the temporary UUID generated when each Job Center Worker starts.

- Creation time of the Job and each subtask

  The creation time of the Job and the subtasks under the Job. The creation time of the Job is the time when the Job is submitted to the database; the creation time of subtasks under the Job is the time when the Splitter finishes analyzing and writes them into the database.

- Last modification time of the Job and each subtask

- Completion time of the Job and each subtask

  The completion time of a subtask under the Job should be the time when the individual task completes; the completion time of the Job is the time when all tasks in the entire Job have completed.

Job Recovery rules:

- Check all running and non-running Jobs every minute;

- Each Job and each subtask under the Job must record allocation time, execution time, and Handler ID;

- If the Handler is no longer running, resubmit the Job or subtask to Job Center for processing;

- When the Handler has not been written for more than 5 minutes: if it is a Leader task, resubmit it; if it is a Follower task, submit the corresponding task to Job Center for processing. If a subtask is assigned to a specific node but the node does not respond, mark that subtask as failed;

- If all subtasks of a Job have been executed, but the Job has not been marked completed or failed for more than 1 minute, resubmit the Job to Job Center for processing;

- If the task message sent to Job Center is duplicated, do not resubmit it; after a task is marked failed, clear the waiting or unfinished messages;

- When determining the type of a Job that needs to be resubmitted as described above and it is Scheduler, the Job will not be resubmitted and the entire Job and unfinished subtasks will be marked as Failed, to prevent a large number of scheduled tasks from continuously retrying.
