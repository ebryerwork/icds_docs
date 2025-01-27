# Using the Web Portal

ICDS offers an interactive web portal powered by [Open OnDemand](https://openondemand.org/)
which allows users access to graphical file handling features, graphical desktop software and
interfaces, and popular Integrated Developer Environments (IDEs) such as Jupyter Notebooks and RStudio.

For an in-depth overview of Open OnDemand features, see [this tutorial video](https://youtu.be/w1hbOppyUUc?si=Ubv0ymfeZmnD7Kzr)
developed by [The Yale Center for Research Computing](https://research.computing.yale.edu/)

## Selecting Resources for Interactive Jobs

Interactive jobs and scheduled and managed by Slurm and require resource definitions similar to
batch jobs. This means the amount of cores, memory (RAM), and run-time need to be specified before
jobs can be started.

To avoid errors, the hardware requested must be accompanied by a compatable account, partition, and node type.
Here are some common use cases and the necessary settings:

To use the open queue:

 - Account: open
 - Partition: open
 - Node type: standard

To use the interactive nodes:

 - Account: open
 - Partition: intr
 - Node type: Interactive

To use paid resources:
 - Account: your_allocation_id
 - Partition: sla-prio
 - Node type: must match the resources in your allocation

!!! warning "All jobs must fit inside the resource limits of the partition they are running on"
     If a job requests resources that exceed the partition limits, they will not begin.


- Open queue jobs must not exceed 100 cores and 800 GB memory
- Interactive jobs must not exceed 4 cores and 24 GB memory
- Paid resource limits are definied by the allocation limits

## Custom Environments

To use custom software, such as Anaconda environments or custom software modules,

