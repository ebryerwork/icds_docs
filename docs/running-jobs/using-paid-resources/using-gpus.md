
#### Using GPUs

GPUs are available to users of paid allocations or credit accounts. 
To request GPU resources, use the `--gpus` resource directive:

```
#!/bin/bash

#SBATCH --job-name=apythonjob   # give the job a name
#SBATCH --account=<gpu_acct>    # specify the account
#SBATCH --nodes=1               # request a node
#SBATCH --ntasks=1              # request a task / cpu
#SBATCH --mem=1G                # request the memory required per node
#SBATCH --gpus=1                # request a gpu
#SBATCH --time=00:01:00         # set a limit on the total run time

python pyscript.py
```

For paid allocations, the job will automatically be allocated a GPU that corresponds to the resources in the allocation.

For credit accounts, a specific GPU model can be requested by adding the relevent `--constraint` to the resource request. 
Please note that your resource request must include a hardware partition using the `--partition` or `-p` flags. At this time, 
**only standard core hardware have available GPUs**.

For example, to request an A100 GPU using a credit account to be ran on standard cores

```
#!/bin/bash

#SBATCH --job-name=apythonjob   # give the job a name
#SBATCH --account=<gpu_acct>    # specify the account
#SBATCH --partition=standard    # specify hardware partition
#SBATCH --nodes=1               # request a node
#SBATCH --ntasks=1              # request a task / cpu
#SBATCH --mem=1G                # request the memory required per node
#SBATCH --gpus=1                # request a gpu
#SBATCH --time=00:01:00         # set a limit on the total run time

python pyscript.py
```

Requesting GPU resources for a job is only beneficial if the software running within the job is GPU-enabled. 
Accounts will be billed for GPU usage even if the allocated GPU is not utilized. 

