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
