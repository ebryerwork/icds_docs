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
