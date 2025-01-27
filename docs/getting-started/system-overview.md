# System Overview

Compute clusters like Roar serve many purposes:

- **number crunching**, much bigger and faster than a laptop
- **batch compute jobs**, submitted and performed later
- **interactive computing**, on the equivalent of a powerful workstation
- **large-scale storage** and access of data files

Roar consists of two clusters:  **Roar Collab**, and **Roar Restricted**.
Roar Collab is for general use;
Roar Restricted is only for users working with sensitive data requiring extra security provisions.  
For details, see the [Roar Restricted](16_RoarRestricted.md) addendum.

## Architecture

Collab consists of different parts, connected together by networks:

- **users** of the cluster, who connect to either
- **submit nodes**, to prepare and submit jobs, or
- **the Portal**, for interactive computing;
- **file storage** for user files, plus
- **scratch storage** for temporary files; and 
- **compute nodes**, of several different types.

![architecture](img/RCUserFlowDiagram.png)

## Accounts

To log on to Collab, you need a [login account](04_LoginAccounts.md).
To work on Collab, you can use the open queue at no cost,
which gives you access to the Portal, and to batch jobs on vintage hardware.
But to use any of the newer, more powerful hardware,
you need a paid [charge account](05_ChargeAccounts.md).

## Accessing Roar

Roar Collab can be accessed in two ways: via the web-based Collab Portal <br>
<https://rcportal.hpc.psu.edu/pun/sys/dashboard> <br>
and by "secure shell" ([`ssh`][ssh]) 
from a terminal application.
[ssh]: https://linux.die.net/man/1/ssh

The Portal (which runs [Open OnDemand](https://openondemand.org))
is designed mainly for interactive work.
It provides:

- a Windows-like desktop environment;
- a web-based file browser, to upload and download files;
- graphical, number-crunching programs, 
such as ANSYS, COMSOL, MATLAB, and RStudio.

The Portal is easy to use, 
because its preloaded programs can be launched and used
without knowing Unix.
And, its Windows-like desktop provides a familiar "feel"
for users accustomed to laptops (especially Linux laptops).
From its Terminal application, users have access to the full capabilities of Collab, needed to prepare and submit jobs.

Collab can also be accessed via SSH (Secure SHell), from a terminal application on a laptop. 
For more information about Portal and SSH access, see [Connecting to Roar Collab](../getting-started/connecting-to-rc).
