# Software modules

Collab provides many different applications in its software stack,
which consists of two parts:

- preloaded software, available immediately on login;
- modular software, which must be loaded to be used.

Not all software is preloaded,
because conflicts inevitably arise 
between different versions of libraries
used by different software packages.
Loading only certain software by modules
is an attempt to manage this chaos.

To find out if an application is available, use `which`:
```
which <appName>
```
which returns the path to the executable `<appName>`,
if it exists on your `$PATH`.
(The $PATH variable contains the set of directories
where Unix looks for executables;
defaults for $PATH are initialized at logon.)

If which doesn’t find the app you are looking for,
it may need to be loaded via the `module` system.
Here are the various commands to search for,
get info on, list, load, and unload modules:

| Command | Description |
| ---- | ---- |
| `module avail` | List all modules |
| `module show <module_name>` | Show module file contents |
| `module spider <module_name>` | Search for a module |
| `module load <module_name>` | Load a module |
| `module load <module>/<version>` | Load a specific version |
| `module unload <module_name>` | Unload a module |
| `module list` | List all loaded modules |
| `module purge` | Unload all modules |
| `module use <path>` | Add a path to `$MODULEPATH` |


What module files mainly do is add various directories 
to the paths Unix searches when looking for applications.
To see what a given modulefile does, use `module show <moduleName>`.

!!! tip ""
     Batch files must include `module load` commands to load the modules they need.
     Modules you have loaded when you submit a job with `sbatch` are not inherited by the job.
