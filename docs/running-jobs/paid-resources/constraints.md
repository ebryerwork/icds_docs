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
