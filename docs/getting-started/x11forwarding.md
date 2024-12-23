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
