# File storage

Files are stored on Roar in a central filesystem;
Collab and Restricted filesystems are separate.

Users have access to four directories:  home, work, group, and scratch.
These have different purposes:

- **home** – for configuration files, and links to work, group, and scratch.
- **work** – for your own work; 
only you have read-write access to your home and work directories.
- **group** – for collaborative work.  group space is owned by a PI;
by default, group members have read access to all files in group.
Space in group is not free, and is sold in 5 TB increments.
- **scratch**  – for temporary storage of large files.  scratch is *not backed up*, 
and files older than 30 days are *automatically deleted*.

Files in home, work, and group are backed up by a sequence of daily "snapshots". 
Snapshots are not saved beyond xxx days.
If you mistakenly delete a file, you can request it to be restored from a snapshot.
Try to avoid this.

## Archive storage

To store infrequently-used files, low-cost archive storage can be purchased. 
The Collab Archive is only accessible via the [Globus][globus] web interface,
so access is not quick or convenient.
If you store a directory that contains many files, 
you should pack the directory into a single file with `tar`
(see [Packing files](12_TransferringFiles.md#packing-files))
before transferring.
[globus]: 12_TransferringFiles.md#globus

## Quotas

home, work, group, and scratch directories are subject to limits,
both on the total filespace and on the total number of files.
On Collab, the limits are:

| Storage | Path | Space | Files | Backup | Purpose |
| :----: | :----: | :----: | :----: | :----: | :----: |
| Home | /storage/home | 16 GB | 500,000 | Daily  | Configuration files |
| Work | /storage/work | 128 GB | 1 million | Daily  | User data |
| Scratch | /scratch | None | 1 million | None | Temporary files |
| Group | /storage/group | Specific to<br>allocation | 1 million <br>per TB | Daily | Shared data |

On Roar Restricted, there is no scratch or group;
otherwise the limits are the same.


## Checking storage

If you fill or nearly fill your home or work directories,
weird errors will result when you try to run programs or write files.
To avoid this, keep an eye on your file sizes and total usage.

There are two tools to check on your disk usage:

- `check_storage_quotas` reports your total usage;
- [`du`][du] reports the sizes of files and directories.
[du]: https://man7.org/linux/man-pages/man1/du.1.html

`du -sh *` gives "human-readable" sizes (in MB, GB, TB) 
for each item in the current directory.

In managing storage, we often want to know where the big files are.
``
du -sh * | sort -h -r
``
lists directory sizes in order from large to small
(the output of du is "piped" to [sort][sort]).
[sort]: https://man7.org/linux/man-pages/man1/sort.1.html

## File permissions

If you are a PI, you have group space on Collab, located at
`/storage/group/<PIuserID>/default`,
for which the default file permissions and ownership are
```
drwxr-s-- 2 root <PIuserID>
```

The `s` setting in the group permissions means 
every file and folder created within the group folder
will have the same group read `r` permission.
However, files created elsewhere and moved into group 
have the permissions they were created with.
To change them, use [`chmod`][chmod]:
[chmod]: https://man7.org/linux/man-pages/man1/chmod.1p.html
```
chmod g+r <filespec>
```
More generally, chmod can be used to add or remove (+ or -) 
permissions to read (r), write (w), or execute (x),
for the user (u), group (g), or others (o).



# Managing files

Common tasks on any filesystem include 
navigating to a directory; listing the files; 
creating folders;
and copying, moving, renaming, and deleting files and folders.
In classic Unix, these tasks are all performed 
with command line tools: 

- `cd` (change directory)
- `ls` (list files) 
- `mkdir` (make directory)
- `rmdir` (remove directory)
- `cp` (copy)
-  `mv` (move)
-  `rm` (remove)

Part of learning [Unix](01_SystemOverview.md#roar-uses-unix)
is becoming facile with these commands.
But if you prefer a more "graphical" user interface,
two options exist.

The [Thunar][thunar] graphical file manager is available
from the Portal Interactive Destop
( menu item Applications/Accessories/Thunar File Manager)
or an SSH -X terminal session (`thunar` at the command line).
[thunar]: https://docs.xfce.org/xfce/thunar/start

Alternatively, the Collab [Portal][portal] top menu under Files/Home
opens a window that enables file management
(moving, copying, renaming, making and deleting folders).
[portal]: https://rcportal.hpc.psu.edu/pun/sys/dashboard

# Finding files

On Macs and PCs, powerful tools exist for finding files
that match certain criteria, or contain certain text.
Two Unix commands that provide similar capabilities 
are [`find`][find] and [`grep`][grep].
[find]: https://man7.org/linux/man-pages/man1/find.1.html
[grep]: https://man7.org/linux/man-pages/man1/grep.1.html

`find` looks for files based on their *attributes* (name, type, size, date),
searches recursively (through all subdirectories of a given directory),
and returns a list of file names.

`grep` looks for files based on their *contents*,
searching locally by default (but can be made to search recursively),
and returns a list of lines that contain the searched-for pattern.

Like many Unix commands, 
find and grep have many option that expand their capabilities,
and can be combined with other Unix commands 
using pipes (`|`) and redirection (`>`) to perform complex tasks.

Tutorials exist for [Unix][unix_tutorial2], 
[grep][grep_tutorial], and [find][find_tutorial].
Google searches on these commands are often helpful
(e.g., "Unix how to find and delete large files").
Here are a few examples of each.
[unix_tutorial2]: https://www.tutorialspoint.com/unix/unix_tutorial.pdf
[grep_tutorial]: https://danielmiessler.com/p/grep/
[find_tutorial]: https://snapshooter.com/learn/linux/find

### find

Find all files with name that matches a pattern:
```
find . -name "*.trr"
```

Find files above a certain size:
```
find . -type f -size +100G
```

Find has a powerful option `-exec`,
which executes a command on files that are found.  
Use this with caution!  List the files first.

Find files, and then compress them:
```
find . -name "*.trr" -exec compress {} ; 
```

Find files of a certain type, get their sizes, and sum them:
```
find . -name "*.trr" -exec du -csh '{}' +
```

Find files of a certain type, get their sizes, and sort by size:
```
find . -name "*.trr" -exec du -sh '{}' + | sort -h -r
```

Find files above a certain size and list them: 
```
find . -type f -size +100G -exec ls -lh {} +
```

Find files of a certain extension and delete them: 
```
find . -name "*.trr" -exec rm -f {} +
```

### grep

In its simplest form, grep searches for a "pattern"
in a given file or set of files:
```
grep <pattern> <file>
```

In this form, grep finds all lines in `<file>` that contain `<pattern>`.
The pattern can have "wildcards" -- `*` matches anything, for example.

`<file>` can be a single filename, or itself a pattern
that matches multiple files; for example, `*.log` matches all logfiles.

grep is often useful to "filter" the output of commands.
`ps -e` lists all running processes (a very long list).
To look for any process that mentions `vmd`:
```
ps -e | grep vmd
```
`grep -R` searches recursively through subdirectories.
Here, grep searches the current directory `.` and its subdirectories,
including all files `*.sh`, looking for pattern `sed`, 
and writes the results to `sedExamples`: 
```
grep -R ‘.’ --include *.sh -e ‘sed’ > sedExamples
```
# Transferring files

Computational workflows often require files 
on Roar Collab, Roar archival storage, 
OneDrive, or your laptop or desktop machine
to be transferred -- copied from one place to another.

Transfers to and from Roar Restricted follow a special protocol,
described [here](16_RoarRestricted.md).

Multiple tools exist to perform these file transfers.
No single tool is best for all cases;
below, we recommend methods, 
and list approximate transfer rates for large files.

| Transfer | Method | Rate (MB/sec) |
| ---- | ---- | ---- |
| Collab &harr; Archive | Globus | 50 |
| Collab &rarr; OneDrive | Firefox or Globus | 50 | 
| OneDrive &rarr; Collab | Firefox or Globus | 10 |
| Collab &harr; laptop | Portal Files menu | 25 |
| Collab &harr; laptop | Cyberduck or FileZilla | 15 |
| OneDrive &harr; laptop | web access |20 |

## Firefox

The Firefox browser is available either 
from the [Portal Interactive Desktop][portalID]
or from an [SSH -X session][sshx].
From Firefox, you can access OneDrive
and other similar destinations,
and perform file transfers.
[portalID]: 06_AccessingCollab.md
[sshx]: 06_AccessingCollab.md#access-via-ssh

## Portal Files menu

The Collab [Portal][portal] top menu under Files/Home
opens a window that enables convenient file transfer 
between Collab and your laptop.
[portal]: https://rcportal.hpc.psu.edu/pun/sys/dashboard

## sftp

[`sftp`][sftp] (secure file transfer protocol) is a Unix tool
for file transfers.  To launch sftp,
[sftp]: https://man7.org/linux/man-pages/man1/sftp.1.html
```
sftp <username>@<address>
```
where `<address>` is the address of a "remote machine",
and `<username>` is your userid on that machine.
For sftp *to* Collab, the address is `submit.hpc.psu.edu`,
the same as for ssh logon.

Just as for ssh logon, you will be prompted 
for your password on the remote machine,
and multi-factor authentication (MFA)
if the remote machine requires it.

sftp is an interactive program.
Once logged on, you can copy files 
from the local machine to the remote with `put <filename>`,
and from the remote machine to the local with `get <filename>`.

When sftp launches, your location on the local machine
is the folder in which you launched sftp,
and your location on the remote machine is your home directory.
To control where on the remote machine files go to and come from,
within sftp you can navigate on the remote machine with `cd`
and list files with `ls`. 
Likewise, within sftp you can navigate on the local machine
with "local" versions of these commands, `lcd` and `lls`.

!!! tip ""
     "Graphical" sftp clients for your laptop
     can be used for file transfer to Collab, 
     as well as to OneDrive or other cloud storage providers.
     Two popular options for both OS X and Windows are
     [Cyberduck][cyberduck] and [FileZilla][filezilla].
[cyberduck]:https://cyberduck.io
[filezilla]:https://filezilla-project.org

## Globus

Globus is a web-based tool for file transfers,
which can move files from Roar Collab
to filesystems at institutions outside Penn State,
including our OneDrive accounts.
To get started, go [here][globus].
[globus]: https://docs.globus.org/how-to/get-started/

Globus moves files between named "endpoints":

| Filesystem | Endpoint |
| ---- | ---- |
| Collab | PennState_ICDS_RC |
| Archive | PennState_ICDS_Archive | 
| PSU OneDrive | "Penn State OACIOR OneDrive Collection 01" |

Globus is interactive, 
but time-consuming file transfers 
can be submitted as batch jobs.

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

## rsync

Sometimes, you want to copy a directory of files 
from one place to another,
and then later *update* the copy
with any changes made to the originals,
so that the copy reflects the current version.
If the directory contains many files but only a few are changed,
it would be nice to have a program that automatically updates
only the changed files. [`rsync`][rsync] does this:
[rsync]: https://linux.die.net/man/1/rsync
```
rsync <options> <source-path> <destination-path>
```
copies files from `<source-path>` to `<destination-path>`,
*and deletes files if necessary*,
to make the destination the same as the source.
Later, if you change files on `<source-path>`,
run rsync again to update files on `<destination-path>`.

rsync has several important options:

- `a` – "archive" mode; traverses directories recursively
- `v` – "verbose"; reports which files are copied
- `z` – "zips" (compresses) the files on transfer
- `h` – "human readable" reporting

The source and destination can be on the same filesystem,
or they can be different machines entirely.
From a Unix command line on your laptop 
(running Linux or OS X),
```
rsync /work/newData abc123@submit.hpc.psu.edu:/storage/work/abc123/toAnalyze/
```
which will prompt for your password and MFA.

Note that the *destination* pathnames end with a `/`;
this signifies that the copied files will go into the folder `toAnalyze`.
For more examples, visit [Tecmint][tecmint].
[tecmint]: https://www.tecmint.com/rsync-local-remote-file-synchronization-commands/

!!! warning ""
     With rsync, the source is the original, and the destination is the copy.
     Don't reverse direction, or you will confuse rsync and yourself,
     and wind up clobbering or deleting files.
