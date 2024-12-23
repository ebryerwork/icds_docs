# File storage

Files are stored on Roar in a central filesystem;
Collab and Restricted filesystems are separate.

Users have access to four directories:  home, work, group, and scratch.
These have different purposes:

- **home** – for configuration files, and links to work, group, and scratch.
- **work** – for your own work; 
only you have read-write access to your home and work directories.
- **scratch**  – for temporary storage of large files.  scratch is *not backed up*, 
and files with a last modified time stamp older than 30 days will be *automatically deleted*.

Additionally, PI-owned **group** storage directories are availalbe for purchase. These are designed for collaborative work or group level software.

Files in home, work, and group are backed up by a sequence of daily "snapshots" which are kept for 90 days.  To have files restored from a snapshot, email Client Support at icds@psu.edu


## Archive storage

To store infrequently-used files, low-cost archive storage can be purchased. 
Archive is only accessible via the [Globus][globus] web interface,
so access is not quick or convenient.
If you store a directory that contains many files, 
you should pack the directory into a single file with `tar`
(see [Packing files](12_TransferringFiles.md#packing-files))
before transferring.
[globus]: 12_TransferringFiles.md#globus

!!! warning "Archive storage is not suitable for storing protected data."
     If you are working with data or software that must adhere to regulatory requirements
     please contact us or the [Office of Information Security](https://security.psu.edu) 
     to ensure it is being handled appropriately.

## Quotas

home, work, group, and scratch directories are subject to limits,
both on the total filespace and on the total number of inodes. Inodes are data structures that 
store most of the essential information about a file or directory. Files, directories, and 
symlinks all count towards inode limits.

On RC, quota limits are:

| Storage | Path | Size | Inodes | Backup | Purpose |
| :----: | :----: | :----: | :----: | :----: | :----: |
| Home | /storage/home | 16 GB | 500,000 | Daily  | Configuration files |
| Work | /storage/work | 128 GB | 1 million | Daily  | User data |
| Scratch | /scratch | None | 1 million | None | Temporary files |
| Group | /storage/group | Specific to<br>allocation | 1 million<br>per TB | Daily | Shared data |

On Roar Restricted, quota levels are the same, however users do not have access to a scratch 
directory and group storage directories are located in the restricted storage space (/restricted/group).


### Solution to common quota issues in home

Many user level config files and package libraries are stored in the home directory by default.
Large package libraries can quickly overwhelm the home quota and cause out of space errors. 
This commonly occurs with directories such a

 - `.local` - used by Python to store user installed packages
 - `.conda` - used by Anaconda to store package caches and user-level environments
 - `.comsol` - used by Comsol

These [dot files](https://missing.csail.mit.edu/2019/dotfiles/) are hidden by default. You can view
them via the command line using the `ls -la` command.

To correct the out of space error, it is recommended to move the offending directory to work and create 
symlink pointing to the new location. For example, moving the `.conda` directory is done with the following commands:

```
mv ~/.conda $WORK/.conda
ln -s $WORK/.conda ~/.conda
```

This can be repeated for any directory in home that is causing the out of space error.


## Checking storage

If you fill or nearly fill your home or work directories,
weird errors will result when you try to run programs or write files.
To avoid this, keep an eye on your file sizes and total usage.

The `quota_check` utility reports total usage for all storage locations 
available to your account.

To see the breakdown of file and directory size, [`du`][du] can be used
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


group space on Collab, located at
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



