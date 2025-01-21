### Requesting Resources

The resource directives should be populated with resource requests that are adequate to complete the job but should be minimal enough that the job can be placed somewhat quickly by the scheduler. 
The total time to completion of a job is the sum of the time the job is queued plus the time it takes the job to run to completion once placed. 
The queue time is minimized when the bare minimum amount of resources are requested, and the queue time grows as the amount of requested resources grows. 
The run time of the job is minimized when all the computational resources available to the job are efficiently utilized. 
The total time to completion, therefore, is minimized when the resources requested closely match the amount of computational resources that can be efficiently utilized by the job. 
During the development of the computational job, it is best to keep track of an estimate of the computational resources used by the job. 
Add about a 20% margin on top of the best estimate of the job's resource usage to produce practical resource requests used in the scheduler directives.

It's useful to examine the amount of resources that a single laptop computer has, or **1 laptop-worth of resources**, as a reference. 
A modern above-average laptop, for example, may have an 8-core processor and 32 GB of RAM. 
If a computational task can run on a laptop without crashing the device, then there is absolutely no need to submit a resource request larger than this unless the job can efficiently utilize the additional resources.

