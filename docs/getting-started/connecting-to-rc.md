# Connecting to Roar Collab

## Setting up a Login Account

Access to Roar Collab (RC) requires a login account.
All RC users have access to user-level [storage space](10_FileStorage.md/#quotas),
and free access to the open queue.

For access to the restricted system, please see the [Roar Restricted Addendum](16_RoarRestricted.md).

Anyone with a Penn State access ID can request an account on Roar Collab.
Students and postdocs must be sponsored by a Penn State faculty member (their supervisor, advisor or collaborator). 

To request an account, fill out the [account request form](https://accounts.hpc.psu.edu/users/).
Once approved, you can connect to RC using your PSU credentials.

## Non-PSU Collaborators

Penn State faculty can set up [sponsored access accounts](https://security.psu.edu/services/penn-state-accts/sponsored/) 
for external collaborators, which provides them with a Penn State access account and email address.
Once the sponsored access account is active, a Roar Collab account can be requested as described above.

## Connecting via the Web Portal

For those who prefer an interactive "point and click" interface, the Web Portal (which runs Open OnDemand) provides:

 - a web-based file browser, for basic file editing and transfer
 - interactive computing using graphical desktop and popular software interfaces such as ANSYS, COMSOL, MATLAB, VS Code, Jupyter, and RStudio
 - a desktop environment (the "RHEL 8 Interactive Desktop") with a "look and feel" familiar to Windows users

The portal provides a solution for users who are not familiar with the Linux command line and who want the interactivity provided by the graphical interface.

Connect to the portal using your web browser at (https://portal.hpc.psu.edu)

For more advanced tasks, users can access the command line interface through the portal under the "Clusters" menu:
[img/RCPortalShell.png]

## Connecting via SSH

Alternatively, you can access the cluster via [SSH](https://linux.die.net/man/1/ssh) from a terminal application running on your laptop.

On Windows, use the Command Prompt included by default. Or install an external SSH client such as [PuTTY](https://www.putty.org) or [MobaXterm](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://mobaxterm.mobatek.net/);

On MacOS, Terminal is installed by default. But you can use an external client such as [iTerm](https://iterm2.com).

From the Command Prompt/Terminal, log on to a submit node using the command
```
ssh <user>@submit.hpc.psu.edu
```

Authenticate using your PSU Credentials, then multi-factor authentication (MFA) which is often a push notification to your cell phone.

To make changes to your MFA device or method please visit [PSU's accounts portal](https://accounts.psu.edu/2fa).

## Connecting to RR

For security reasons, Roar Restricted can only be accessed via the [RR Portal](https://rrportal.hpc.psu.edu/) using the 
[Penn State VPN](https://pennstate.service-now.com/sp?id=kb_article_view&sysparm_article=KB0013431&sys_kb_id=24f7cdd9dbd7e0d02c4f9e74f3961967&spa=1). 
For more details, see the [Roar Restricted Addendum](16_RoarRestricted).

## X Window apps

To use any application that "opens a window"
(called an  "X Window" or "X11" application), 
you need an additional program on your laptop.
On the Mac, this is XQuartz, available [here](https://www.xquartz.org).
On the PC, you need VcXsrv, available [here](https://sourceforge.net/projects/vcxsrv/).

To use cluster applications that open windows, log on with
option `-X` for "X forwarding":
```
ssh -X <user>@submit.hpc.psu.edu
```
When you log on to Collab from somewhere off campus,
X Window apps can sometimes be slow;  
Portal works better in such circumstances.
