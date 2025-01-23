# Compute Allocations

A paid compute allocation provides access to specific compute resources for an individual user or for a group of users. 

A paid compute allocation provides the following benefits:

- Immediate job start for resources up to the allocation limits
- Run times longer than the 48 hour limit on the open queue
- No preemption

## Using an Allocation on the Portal

To utilize an allocation on the Portal, select the desired account name under the "Account" drop down box in 
the Interactive Session request form.

If the account does not appear in the "Account" drop down box, you may need to be added to the allocation. Allocation 
coordinators can [add and remove users from their allocations](managing-accounts.md), or contact the helpdesk at
[icds@psu.edu] to request a user be added.


## Using an Allocation on the Command Line

To submit a job to a paid compute account, supply the `--account` or `-A` resource directive with the compute account name. 
Within a batch script that would look like:

```
#SBATCH -A <compute_account>
```

Or you can provide it as a flag to an `sbatch` command to submit a batch job:

```
sbatch -A <compute_account> <submit_script>
```

Or as a flag to an `salloc` command to request an interactive command line session:

```
salloc -A <compute_account>
```

## Monitoring Allocation Access

The `mybalance` command on Roar lists accessible compute accounts and resource information associated with those compute accounts. 

Use the `mybalance -h` option for additional usage information.

If the account does not appear in the `mybalance` output, you may need to be added to the allocation. Allocation 
coordinators can [add and remove users from their allocations](managing-accounts.md), or the allocation owner can contact the helpdesk at
[icds@psu.edu] to request a user be added.
