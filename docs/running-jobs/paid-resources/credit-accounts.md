# Compute Credit Accounts

A credit account provides access to a variety compute resources for an individual user or for a group of users 
on a pay-per-use basis. 

A credit account provides the following benefits:

- Access to a variety of both CPU and GPU hardware resources
- Run times longer than the 48 hour limit on the open queue
- Pay only for the resources used

## Available Hardware Partitions

Jobs submitted using a credit account can utilize a variety of the CPU and GPU resources in Roar Collab. 
Unlike an [allocation account](allocations.md), a credit account job must also specify the hardware it wants to utilize.

This is done by selecting a hardware partition to run on. Available options are:

- `basic`: Basic core resources (4 GB/core, Ethernet networking)
- `standard`: Standard core resources (8 GB/core, Infiniband connectivity)
- `himem`: High memory core resources (20 GB/core, Infiniband connectivity)

For CPU resources, credit accounts are charged based on the number of cores used and the runtime of the job. 
The number of cores equates to the number of requested cores, or their equivalent memory amount.

For example, if a job requests 1 core with 32 GB memory in the `standard` partition, it will be charged as if 4 
cores were used because it used the memory equivalent of 4 standard cores at 8 GB/core.

## Using a Credit Account on the Portal

To utilize a credit account on the Portal, select the desired account name under the "Account" drop down box in 
the Interactive Session request form.

If the account does not appear in the "Account" drop down box, you may need to be added to the allocation. Allocation 
coordinators can [add and remove users from their allocations](managing-accounts.md), or contact the helpdesk at
[icds@psu.edu] to request a user be added.

Additionally, a hardware partition will need to be specified. To do so, select the "Enable advanced Slurm options" option and 
enter the necessary directives in the "Sbatch options" text box:

```
--partition=<desired_partition>
```

### Requesting GPUs

To request a GPU for the job, you will need to add the `--gpus` directive to specify the desired hardware:

```
--partition=<desired_partition>
--gpus=1
```

You can also request a specific GPU model by using the `--constraint` directive:

```
--partition=<desired_partition>
--gpus=1
--constraint=a100
```

#### VirtualGL GPU acceleration

The VirtualGL GPU acceleration option will ensure the job is launched using OpenGL. This option is beneficial if your 
interactive job uses a graphical interface and requires a GPU to use.

** Please note: If you try to launch a job with the VirtualGL option enabled without requesting a GPU, the job will fail. **


## Using an Allocation on the Command Line

To submit a job using a credit account, supply the `--account` or `-A` resource directive with the credit account name, 
along with the desired hardware `--partition`.
 
Within a batch script that would look like:

```
#SBATCH --account=<compute_account>
#SBATCH --partition=<hardware_partition>
```

Or you can provide it as a flag to an `sbatch` command to submit a batch job:

```
sbatch -A <compute_account> -p <hardware_partition> <submit_script>
```

Or as a flag to an `salloc` command to request an interactive command line session:

```
salloc -A <compute_account> -p <hardware_partition>
```

### Requesting GPUs

All GPUs on Roar Collab available for credit accounts are hosted within the `standard` partition.

To request a GPU for a job running against a credit account, you will need to specify the `standard` partition and 
request GPUs with the `--gpus=n` directive, where `n` is the number of GPU cards desired. Within a batch script, this 
would look like:

```
#SBATCH --account=<credit_account_id>
#SBATCH --partition=standard
#SBATCH --gpus=n
```

Or you can specify this along with your `sbatch` command when submitting jobs:

```
sbatch -A <credit_account_id> -p standard --gpus=n <batch_script>
```

For an interactive job, the `salloc` command is similar:
```
salloc -A <credit_account_id> -p standard --gpus=n
```

Total credit billing for GPU jobs will be a combination of the CPU and GPU usage.


#### Requesting specific GPU models

There are several different models of GPUs available on RC, most of which can be used for credit account jobs. These include:

- `p100` - NVIDIA P100 GPU (1 card per node)
- `v100` - NVIDIA V100 GPU (1 card per node?)
- `a100` - NVIDIA A100 GPU (2 cards per node)
- `a100_3g` - NVIDIA A100 MIG 1/2 slice
- `a100_1g` - NVIDIA A100 MIG 1/7 slice

To request one of the above, in addition to specifying the partition and gpus directives as specified above, the `--constraint` 
directive can be used. 

For example, to request a single A100 GPU the following directives would be needed in your batch script

```
#SBATCH --account=<credit_account_id>
#SBATCH --partition=standard
#SBATCH --gpus=1
#SBATCH --constraint=a100
```

## Monitoring Allocation Access

The `get_balance` command can be used to show current credit account balances. To use, supply the credit account name:

```
get_balance <credit_account>
```

There are options for viewing the output in different units. Use `get_balance -h` for additional usage information.
