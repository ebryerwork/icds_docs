### Compute Allocations

A paid compute allocation provides access to specific compute resources for an individual user or for a group of users. 
A paid compute allocation provides the following benefits:

- Guaranteed job start time within one hour
- No job preemption for non-burst jobs
- Burst capability up to 4x of the allocation's compute resources

A compute allocation results in the creation of a compute account on Roar. 
The `mybalance` command on Roar lists accessible compute accounts and resource information associated with those compute accounts. 
Use the `mybalance -h` option for additional command usage information.

To submit a job to a paid compute account, supply the `--account` or `-A` resource directive with the compute account name and supply the `--partition` or `-p` resource directive with `sla-prio`:

```
#SBATCH -A <compute_account>
#SBATCH -p sla-prio
```

To enable bursting, if enabled for the compute account, supply the `--partition burst` or `-p burst` resource directive.
Furthermore, the desired level of bursting for the job (`burst2x`, `burst3x`, `burst4x`, and so on) must be specified using the `--qos` resource directive. To enable 2x bursting for a batch job, for example, use the following resource directives:

```
#SBATCH -A <compute_account>
#SBATCH -p burst
#SBATCH --qos burst2x
```

To list the available compute accounts and the associated available burst partitions, use the following command:

```
$ sacctmgr show User $(whoami) --associations format=account%30,qos%40
```


#### Modifying Allocation Coordinators

The principal contact for a compute allocation is automatically designated as a coordinator for the compute account associated with the compute allocation. 
A coordinator can add or remove another coordinator with the following command:

```
$ sacctmgr add coordinator account=<compute-account> name=<userid>
$ sacctmgr remove coordinator account=<compute-account> name=<userid>
```


#### Adding and Removing Users from an Allocation

A coordinator can then add and remove users from the compute account using the following:

```
$ sacctmgr add user account=<compute-account> name=<userid>
$ sacctmgr remove user account=<compute-account> name=<userid>
```


#### Available Compute Resources

A paid compute allocation will typically cover a certain number of cores across a certain timeframe. 
The resources associated with a compute allocation are in units of **core-hours**. 
The compute allocation has an associated **Limit** in **core-hours** based on the initial compute allocation agreement. 
Any amount of compute resources used on the compute allocation results in an accrual of the compute allocation's **Usage**, again in **core-hours**. 
The compute allocation's **Balance** is simply the **Limit** minus its **Usage**.

```
Balance [core-hours] = Limit [core-hours] - Usage [core-hours]
```

At the start of the compute allocation, 60 days-worth of compute resources are added to the compute allocation's **Limit**. 
Each day thereafter, 1 day-worth of compute resources are added to the **Limit**.

```
Initial Resources   [core-hours] = # cores * 24 hours/day * 60 days
Daily Replenishment [core-hours] = # cores * 24 hours/day
```

The daily replenishment scheme continues on schedule for the life of the compute allocation. 
Near the very end of the compute allocation, the replenishment schedule may be impacted by the enforced limit on the maximum allowable **Balance**. 
The **Balance** for a compute allocation cannot exceed the amount of compute resources for a window of 91 days and cannot exceed the amount usable by a 4x burst for the remaining life of the compute allocation. 
This limit is only relevant for the replenishment schedule nearing the very end of the compute allocation life.

```
Max Allowable Balance [core-hours] = min( WindowMaxBalance, 4xBurstMaxBalance )

where

WindowMaxBalance  [core-hours] = # cores * 24 hours/day * 91 days
4xBurstMaxBalance [core-hours] = # cores * 24 hours/day * # days remaining * 4 burst factor
```


