### Interactive Jobs

The submit nodes are designed to handle very simple tasks such as connections, file editing, and submitting jobs. 
Performing intensive computations on submit nodes will not only be computationally inefficient, but it will also adversely impact other users' ability to interact with the system. 
For this reason, users that want to perform computations interactively should do so on compute nodes within an interactive compute session. 
Slurm's [salloc](https://slurm.schedmd.com/salloc.html) command is used to request an interactive compute session. 
To work interactively on a compute node with a single processor core for one hour, use the following command:

```
$ salloc --nodes=1 --ntasks=1 --mem=1G --time=01:00:00
```

Equivalently, short options can be used instead of the long options, so the abbreviated version of this command is instead

```
$ salloc -N 1 -n 1 --mem 1G -t 1:00:00
```

The above commands submit a request to the scheduler to queue an interactive job, and when the scheduler is able to place the request, the prompt will return. 
The hostname in the prompt will change from the previous submit node name to a compute node. 
Now on a compute node, intensive computational tasks can be performed interactively. 
This session is terminated either when the time limit is reached or when the `exit` command is entered. 
After the interactive session completes, the session will return to the previous submit node.
