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
     Batch files must include `module load` commands
     to load the modules they need.
     Modules you have loaded when you submit a job with `squeue`
     are not available to the job itself.

## Automatic loading

On Unix machines, settings are stored in "hidden" text files, 
(names start with `.`, so they don't show up with `ls`),
in your home directory.
Settings files are hidden to keep users from meddling with them.
But one such file that you may want to alter is `~/.bashrc`.

When you log in, commands in .bashrc are automatically executed.
So lines may be added to .bashrc to load modules
for software you use frequently.

!!! tip "" 
     If your .bashrc file contains `module load` commands,
     and your batch script begins with `#!/bin/bash`,
     then your .bashrc file will execute when the batch job starts,
     and the job will have access to the loaded modules.

# Loading packages


## Python 

Python is a widely-used programming language,
preloaded on Collab,
which is greatly extensible in its capabilities
by loading additional packages.

To load Python packages, use pip:
```
pip install --user <package>
```
Python packages are loaded by default into `$HOME/.local`.
If you load a large number of big Python packages,
you may exceed the limited storage space in your home directory.

If this becomes a problem, the `.local` directory can be moved to `~/work`,
and a link placed in your home directory.
To make such a link, in your home directory execute the command
```
ln -s .local work/.local
```
which creates an alias (in Unix-speak, a "symbolic link") named `.local`
that points to the directory you moved to `work`.

## Anaconda

Anaconda is a "package manager",
originally developed for Python, 
but now used by several software platforms
to manage installation of packages.

One such software platform is R,
a widely used application for statistical analysis and plotting,
which is greatly extensible by loading packages.
To use Anaconda to manage the installation of R,
first load its module: 
```
module load anaconda
```
Next, create an Anaconda "environment"
(set of loaded applications and packages),
that contains R as a "base":
```
conda create -y -n <environmentName> r-base
```
If you want some R package always to be loaded,
include it in the list of packages:
```
conda create -y -n <environmentName> r-base r-plot3d r-ggplot
```
To activate an Anaconda environment:
```
conda activate <environmentName>
```
Within an active environment, to load a package, execute
```
conda install <package>
```
This table summarizes useful Anaconda commands:

| Command | Description |
| ---- | ---- |
| `conda create –n <env_name>` | Creates a conda environment by name |
| `conda create –p <env_path>` | Creates a conda environment by location |
| `conda env list` | Lists all conda environments |
| `conda env remove –n <env_name>` | Removes a conda environment  |
| `conda activate <env_name>` | Activates a conda environment |
| `conda list` | Lists all packages in the active environment |
| `conda deactivate` | Deactivates the active environment |
| `conda install <package>` | Installs a package in the active environment |
| `conda search <package>` | Searches for a package |
| `conda env export > env_name.yml` | Save the active environment to a file |
| `conda env create –f env_name.yml` | Loads an environment from a file |

## Anaconda in batch scripts

To ensure that Anaconda is properly initialized 
for use in batch scripts, 
your `.bashrc` file must be executed.
This can be done in one of three ways:

- `source ~/.bashrc`  executes your `.bashrc` file;
- load your environment with `source activate <environmentName>`;
- begin your script with `#!/bin/bash`, which also executes your `.bashrc` file.

## Anaconda on Portal

Special considerations apply if you want to use conda environments you have defined,
for Python or R for example,
in an interactive session launched from the Collab Portal.

### Jupyter Server

The Jupyter Server can be used with a pre-defined Python environment,
which you select from the "Environment type" dropdown menu 
that appears as you configure the session.

To use your own previously created conda environment within a Jupyter Server session,
select instead "Use custom text field", which will contain 
```
module load anaconda3
```
For this to work, the `ipykernel` package must be installed into your environment beforehand.
To do this, within a terminal session execute the following:
```
conda activate <environment>
conda install -y ipykernel
ipython kernel install --user --name=<environment>
```
When the session begins, your environment is displayed in the kernel list.

### RStudio 

Likewise, RStudio can be used with a default environment,
selected from the "Environment selection" dropdown menu.
Furthermore, when the session starts,
additional R packages can be installed from an extensive list.

But if you want to use your own custom environment within an RStudio session,
select instead "Use custom text field", and enter the following text:
```
module load anaconda
conda activate <environment>
export CONDAENVLIB=~/.conda/envs/<environment>/lib
export LD_LIBRARY_PATH=$CONDAENVLIB:$LD_LIBRARY_PATH
```

Notes:

- The export commands help RStudio load some libraries 
while accessing the conda environment's R installation. 
- The default location of conda environments is `~/.conda/envs`.
If your environment is installed somewhere else, 
`CONDAENVLIB` should be set accordingly. 
# Installing from source

Collab offers a broad range of installed open-source applications,
but sometimes you need an application Collab doesn’t have.
When that happens, ask the ICDS Help Desk to install it for you,
particularly if you can make a case that others will also use it.

If that doesn’t work, you may try installing the application yourself,
in your own work or group directory.
Depending on the application,
and how well its source package is designed and documented,
this can be relatively straightforward, or a total nightmare.

The nightmare scenarios involve poor documentation,
combined with the need for other packages also not installed on Collab,
which in turn need other packages, and so on.

## No root access

If you have worked with a laptop running Linux,
one important difference between installing software 
on your laptop and on Collab is **no root access**.
This means you cannot:

- use RPM package installers like [`yum`][yum]
- install executables in the standard places
[yum]: https://man7.org/linux/man-pages/man8/yum.8.html

## wget

The first step is to get the source package (typically a tarball of some sort)
from the developer website onto Collab.
If you are logged on with Interactive Desktop or an SSH -X session, 
you can launch Firefox and download software using the browser.

Alternatively, you can use [`wget`][wget],
to download source packages from the web:
[wget]: https://linux.die.net/man/1/wget
```
wget <webAddress>
```
where `<webAddress>` can be copied from a browser link pointing to the file.
Then, **read the README files**, and see what you are up against.

## cmake

Many source packages are built using [`cmake`][cmake],
a Unix tool for controlling the compile and load process.
To use cmake, first load its module:
[cmake]: https://cmake.org/cmake/help/latest/manual/cmake.1.html
```
module load cmake
```
To build from source, the typical procedure
is to `cd` into the source folder,
and execute in turn:
```
mkdir build
cd build
cmake <options>
make
make install
```
Here `<options>` is a list of options for cmake,
that may control what version of the software to build,
what assumptions to make about the CPU,
what packages to include,
and where to install the resulting executables.
Well-designed source packages include help files
that describe the various build options.

## Group access

If you want others to be able to use 
software that you build from source,
the executables and libraries generated by the build
must be placed in a directory that others can access.

The simplest way to achieve this 
is to place the executables in your group space.
Group space for a PI on Collab is located at
`/storage/group/<PIuserID>/default`,
which is read-accessible by members of `<PIuserID>_collab`.
Note however that if a PI makes an alias 
to their group space in their home directory,
with the command
```
ln -s group /storage/group/<PIuserID>/default
```
the path `/storage/home/<PIuserID>/group` 
is *not* accessible to others,
because their home directory `/storage/home/<PIuserID>`
is not accessible to others.


## Custom modules

To use software you have compiled from source,
it is convenient to make your own modulefile,
for which it is helpful to have an example.
Modulefiles on Collab are located primarily 
in `/storage/icds/RISE/sw8/modules`.

The contents of a modulefile are:

- "whatis" directives,
that supply information for `module info` and `module spider`;
- possibly some "load" commands 
to load other modules needed by the given module;
- changes to various path variables,
so the system can find the software.

Here is an example:

```
whatis([[Name : gromacs]])
whatis([[Version : 2024.3]])
whatis([[Target : haswell]])

whatis([[Description : GROMACS is a versatile molecular dynamics package.]])
whatis('URL: https://www.gromacs.org')

whatis([[Configure options: -DGMX_MPI=off 
-DCMAKE_INSTALL_PREFIX=/storage/icds/RISE/sw8/gromacs/gromacs-2024.3/install 
-DGMX_DOUBLE=off -DGMX_BUILD_OWN_FFTW=ON -DGMX_GPU=off]])

help([[This GROMACS version was built on 10/22/2024 on p-sc-2370, using the gcc
v13.2.0 compilers with openmpi v5.0.3 and cuda toolkit v12.6.2.]])

-- Local variables
local base = '/storage/icds/RISE/sw8/gromacs/gromacs-2024.3/install'

-- Additional modules
load('gcc/13.2.0')
load('cuda/12.6.2')
load('openmpi/5.0.3')

-- Take care of $PATH, $LD_LIBRARY_PATH, $MANPATH etc
prepend_path('PATH', pathJoin(base,'bin'))
prepend_path('MANPATH', pathJoin(base,'share/man'))
prepend_path('LD_LIBRARY_PATH', pathJoin(base,'lib64'))
prepend_path('LIBRARY_PATH', pathJoin(base,'lib64'))
prepend_path('C_INCLUDE_PATH', pathJoin(base,'include'))
prepend_path('CPLUS_INCLUDE_PATH', pathJoin(base,'include'))
prepend_path('CPATH', pathJoin(base,'include'))
prepend_path('PKG_CONFIG_PATH', pathJoin(base,'lib64/pkgconfig'))
```

To tell the system where to find your custom modules,
add this line to your `.bashrc` file:
```
module use <module_directory>
```
in which `<module_directory>` is the path to your modules.

To make custom modules accessible to your group, 
place them in your group folder.
Group members should likewise include `module use...` in their `.bashrc` files.
