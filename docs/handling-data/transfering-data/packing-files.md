## Packing files

To transfer many files,
or an entire directory of files, possibly with subdirectories,
it is convenient to first make a single large file
of the entire contents,
using the Unix command `tar`
("Tape ARchive", because in ancient days big files
would be archived to magnetic tape).  The command
```
tar -cf <tarfilename>.tar <filespec>
```
creates (`-c`) a single .tar file (`-f`) (sometimes called a "tarball"),
containing the entire contents of `<filespec>`.
With option `-v` (as in `tar -cvf`), tar operates "verbosely",
listing every file added.

To make a tarball of everything in the current directory:
```
tar -cf myTar.tar *
```

tar with option `-z` (as in `tar -czf`)
makes a "zipped" (compressed) tarball.
Compressing text files often makes the tarball much smaller;
compressing binary or image files is usually pointless.

To unpack a tarball (option `-x` for "extract"):
```
tar -xf myTar.gz
```

