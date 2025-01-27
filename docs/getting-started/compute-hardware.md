# Compute hardware

A cluster consists of multiple nodes connected to one or more central filesystems. 
A node is basically a single computer, roughly comparable to a powerful desktop machine. 

Some nodes are networked together with fast connections (Infiniband) that enable 
efficient communication between nodes, allowing large jobs to run in parallel 
on multiple nodes.

Finally, some nodes include GPUs (graphical processing units),
which can accelerate certain compute jobs.

## Node attributes

Roar Collab contains a wide variety of different hardware configurations. To find out 
specifics about the hardware on different nodes, there are several helpful tools.

`lscpu`: displays information about the CPU and its capabilities
`nvidia-smi`: displays information about the GPU (if present).

Using these commands within your jobs can provide details on the hardware it is running
on.

## sinfo

The SLURM command `sinfo` displays information about *all* Collab nodes.
Its output is more easily read with some formatting options,

```
sinfo --Format=features:30,nodelist:20,cpus:5,memory:10,gres:30
```

An example output of the `sinfo` command would look like:
```
$ sinfo --Format=features:30,nodelist:20,cpus:5,memory:10,gres:30
AVAIL_FEATURES                NODELIST            CPUS MEMORY    GRES
standard,a100,cascadelake     p-gc-[3001-3035,303848   380000    gpu:a100:2(S:0-11,36-47)
standard,a100_3g,mig,cascadelap-gc-3036           48   380000    gpu:a100_3g:4(S:0-11,36-47)
```

## Constraints

Paid accounts can fine-tune their resource request using the `--constraint` directive.

From within a submit script, the constraint feature can be used by adding the following to 
your SBATCH header:

```
#SBATCH --constraint=<feature>
```

where `<feature>` is one of the features listed by sinfo (or multiple features, separated by commas).

To request nodes with a given feature for an interactive job,  
add a `-C` option to your `salloc` command:

```
salloc -N 1 -n 4 -A <alloc> -C <feature> -t 1:00:00
```

Any of the "tags" listed in the AVAIL_FEATURES columnfrom the [sinfo output (above)](#sinfo) 
can be used as a constraint to customize your hardware requests. 

For example, to request a job only run on 
`cascadelake` hardware, you would add the following directive to your resource requests:
```
--constraint=cascakelake
```
