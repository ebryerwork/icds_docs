#### R Packages with Anaconda

The R installation itself and its R packages can be easily installed and managed within a conda environment. 
Creating a conda environment containing its own R installation and some R packages can be accomplished with the following:

```
(base) $ conda create -n r_env
(base) $ conda activate r_env
(r_env) $ conda install r-base
(r_env) $ conda install r-tidyverse
```

Note that after `r-base` is the base R installation, and R packages (or in the case of `tidyverse`, a bundle of packages) usually are named `r-*` in conda repos.

Alternatively, the creation of this environment can be completed with a single line.

```
(base) $ conda create -n r_env r-base r-tidyverse
```
