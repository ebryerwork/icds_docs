

### R

R is a free software environment for statistical computing and graphics.


#### R Versions

R users should make sure that the version of R remains consistent. 
Several R versions are available, and when a package is installed in one version, it is not always accessible when operating in another version. 
Always check the R version and remain consistent! 
R modules can be loaded from the central software stack, and R can also be installed by users in a variety of ways within their userspace or group spaces.


#### Install R Packages

R manages some dependencies and versions through the CRAN-like repos. 
R packages can be installed from within the R console with the following command:

```
> install.packages( <package> )
```

Upon running the install command, a warning usually appears stating that the default system install location is not writable, so it asks to install in a personal library instead. 
After entering "yes" as a response, it may then ask to create a personal library location. 
Responding "yes" again will proceed with the installation, probably by asking to select a CRAN repository.

The default personal directory described above will install the package within the `~/R/` directory. 
An install location can instead be supplied to the install command using the `lib` argument:

```
> install.packages( "<package>", lib="<install_location>" )
```

After installation, packages can then be loaded using the following command in the R console:

```
> library( <package> )
```

If the package was installed in a non-standard location, then the package can be loaded from that custom install location using the `lic.loc` argument of the `library()` command:

```
> library( <package>, lib.loc="<install_location>" )
```

Another method to specify package installation locations for R is to modify the `R_LIBS` environment variable before launching an R console session. 
If RStudio is being used, though, the `R_LIBS_USER` environment variable must be modified before launching RStudio. 
Modifying these environment variables properly can eliminate the need to use the `lib.loc` option of R's `library()` command.

It is recommended to review dependencies of any packages to be installed because additional software may have to be loaded in the environment before launching the R console. 
For example, some R packages utilize CMake to perform the installation. 
In that case, the *cmake* module should be loaded before launching the R console session.


#### R Package Installation Example

To install the ggplot2 R package, first search ggplot2 online to see if there are installation instructions. 
A quick search shows that ggplot2 is included in the tidyverse package and that the recommended installation instructions are the following:

```
# The easiest ways to get ggplot2 is to install the whole tidyverse package:
> install.packages("tidyverse")

# Alternatively, install just ggplot2:
> install.packages("ggplot2")
```

Searching for install instructions usually provides all the necessary information!

Some R packages may require changes to the user environment before the package can be installed successfully within the R console. 
Typically, the user environment change is as simple as accessing a newer compiler version by loading a software module like *intel* with

```
$ module load intel
```

Sometimes, installing R packages may be a little more involved. 
To install the *units* R package, for example, an additional library must be downloaded and installed locally for the package to be installed properly. 
To install the *units* R package for R version 4.2.1, perform the following commands in an interactive session on a compute node:

```
$ cd ~/scratch
$ wget https://downloads.unidata.ucar.edu/udunits/2.2.28/udunits-2.2.28.tar.gz
$ tar -xvf udunits-2.2.28.tar.gz
$ cd udunits-2.2.28
$ ./configure prefix=$HOME/.local
$ make
$ make install
$ export UDUNITS2_INCLUDE=$HOME/.local/include
$ export UDUNITS2_LIBS=$HOME/.local/lib
$ export LD_LIBRARY_PATH=$HOME/.local/lib:$LD_LIBRARY_PATH
$ module load r/4.2.1
$ R
> install.packages("units")
> library(units)
```


#### R Packages with Anaconda

The R installation itself and its R packages can be easily installed and managed within a conda environment. 
Creating a conda environment containing its own R installation and some R packages can be accomplished with the following:

```
(base) $ conda create -n r_env
(base) $ conda activate r_env
(r_env) $ conda install r-base
(r_env) $ conda install r-tidyverse
```

Note that after `r-base` is the base R installation, and R packages (or in the case of `tidyverse`, a bundle of packages) usually are named `r-*` in conda repos.

Alternatively, the creation of this environment can be completed with a single line.

```
(base) $ conda create -n r_env r-base r-tidyverse
```

