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
