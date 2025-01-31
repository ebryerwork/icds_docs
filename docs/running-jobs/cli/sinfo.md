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
