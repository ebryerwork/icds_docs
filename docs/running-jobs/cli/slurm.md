
# Jobs with Slurm

The Roar computing clusters are shared computational resources. 
To perform computationally intensive tasks, users must request compute resources and be provided access to those resources. 
The request/provision process allows the tasks of many users to be scheduled and carried out efficiently to avoid resource contention. 
[Slurm](https://slurm.schedmd.com) is utilized by Roar as the job scheduler and resource manager. 
Slurm is an open source, fault-tolerant, and highly scalable cluster management and job scheduling system for Linux clusters. 
Slurm is rapidly rising in popularity and many other HPC systems use Slurm as well. 
Its primary functions are to
 
 - Allocate access to compute resources to users for some duration of time
 - Provide a framework for starting, executing, and monitoring work on the set of allocated compute resources
 - Arbitrate contention for resources by managing a queue of pending work

!!! warning

    Do not perform computationally intensive tasks on submit nodes. Submit a resource request via Slurm for computational resources so your computational task can be performed on a compute node.


## Slurm Resource Directives

Resource directives are used to specify compute resources when submitting a job 
request to the scheduler. They allow you to indicate the run time, amount of memory, 
and the number of cores your job will use. They are required when launching 
[Interactive Jobs]() and [Batch Jobs](#batch-jobs) through the
command line interface.

[Interactive Jobs Through the Roar Portal](#interactive-jobs-through-the-roar-portal) 
also use resource directives through the drop down menus in the portal interface.

The following table lists some of the most commonly used resource directives.

| Short option | Long option | Description |
| ---- | ---- | ---- |
| `-J` | `--job-name` | Specify a name for the job |
| `-A` | `--account` | Charge resources used by a job to a specified account |
| `-p` | `--partition` | Request a partition for the resource allocation |
| `-N` | `--nodes` | Request a number of nodes |
| `-n` | `--ntasks` | Request a number of tasks |
| NA | `--ntasks-per-node` | Request a number of tasks per allocated node |
| NA | `--mem` | Specify the amount of memory required per node |
| NA | `--mem-per-cpu` | Specify the amount of memory required per CPU |
| `-t` | `--time` | Set a limit on the total run time |
| `-C` | `--constraint` | Specify any required node features* |
| `-e` | `--error` | Connect script's standard error to a non-default file |
| `-o` | `--output` | Connect script's standard output to a non-default file |
| NA | `--requeue` | Specify that the batch job should be eligible for requeuing |
| NA | `--exclusive` | Require exclusive use of nodes reserved for job |


* Constraits are only available for paid resources.

Details on additional directives and job options can be found in the [Slurm sbatch documentation]
(https://slurm.schedmd.com/sbatch.html) for batch jobs and the [Slurm salloc documentation]
(https://slurm.schedmd.com/salloc.html) for interactive jobs.

## Replacement Symbols

Replacement symbols can be used inside of slurm directives to populate the 
values with dynamic content for each job, such as the Job ID or the hostname 
of the node the job is running on.

| Symbol | Description |
| :----: | ---- |
| `%j` | Job ID |
| `%x` | Job name |
| `%u` | Username |
| `%N` | Hostname where the job is running |
| `%A` | Job array's master job allocation number |
| `%a` | Job array ID (index) number |

Examle: Both standard output and standard error are directed to the same file by default, 
and the file name is `slurm-%j.out`, where the `%j` is replaced by the job ID. 
The output and error filenames are customizable, however, using the table of 
symbols below.

## Environmental Variables

Slurm makes use of environment variables within the scope of a job, and 
utilizing these variables can be beneficial in many cases.

| Environment Variable | Description |
| ---- | ---- |
| `SLURM_JOB_ID` | ID of the job |
| `SLURM_JOB_NAME` | Name of job |
| `SLURM_NNODES` | Number of nodes |
| `SLURM_NODELIST` | List of nodes |
| `SLURM_NTASKS` | Total number of tasks |
| `SLURM_NTASKS_PER_NODE` | Number of tasks per node |
| `SLURM_QUEUE` | Queue (partition) |
| `SLURM_SUBMIT_DIR` | Directory of job submission |

Further details on the available resource directives for Slurm are defined by Slurm in the documentation 
of the [salloc](https://slurm.schedmd.com/salloc.html) and [sbatch](https://slurm.schedmd.com/sbatch.html) commands.


