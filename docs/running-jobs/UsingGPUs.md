
#### Using GPUs

GPUs are available to users that are added to paid GPU compute accounts. 
To request GPU resources, use the `--gpus` resource directive:

```
#!/bin/bash

#SBATCH --job-name=apythonjob   # give the job a name
#SBATCH --account=<gpu_acct>    # specify the account
#SBATCH --partition=sla-prio    # specify the partition
#SBATCH --nodes=1               # request a node
#SBATCH --ntasks=1              # request a task / cpu
#SBATCH --mem=1G                # request the memory required per node
#SBATCH --gpus=1                # request a gpu
#SBATCH --time=00:01:00         # set a limit on the total run time

python pyscript.py
```

Requesting GPU resources for a job is only beneficial if the software running within the job is GPU-enabled.


