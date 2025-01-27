# Creating custom module files

ICDS uses the lmod Environmental Module system. The contents of a modulefile are:

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

To use your custom modules, use the `module use` command to specify the location of your module files:

```
module use <module_directory>
```
in which `<module_directory>` is the path to your modules.

These files can be placed in group storage to make them accessable to all group members.

Adding the `module use` line to your `.bashrc` file makes the modules accessable upon login.
