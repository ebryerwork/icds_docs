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

