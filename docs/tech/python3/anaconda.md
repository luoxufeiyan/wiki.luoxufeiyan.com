# Anaconda

从`virtualenv`换到了`Anaconda`

```
# For Windows users# Note: <> denotes changes to be made

#Create a conda environment
conda create --name <environment-name> python=<version:2.7/3.5>

#To create a requirements.txt file:
conda list #Gives you list of packages used for the environment

conda list -e > requirements.txt #Save all the info about packages to your folder

#To export environment file
activate <environment-name>
conda env export > <environment-name>.yml

#For other person to use the environment
conda env create -f <environment-name>.yml
```

[To package a conda environment (Requirement.txt and virtual environment)](https://gist.github.com/pratos/e167d4b002f5d888d0726a5b5ddcca57)

## Add channel

添加第三方channel维护的pkg.
```
(COMP9444) gao@Virubuntu:~$ conda config --add channels pytorch
(COMP9444) gao@Virubuntu:~$ conda config --get channels
--add channels 'defaults'   # lowest priority
--add channels 'pytorch'   # highest priority
```

## Remove env

```
conda remove --name myenv --all
```


## Ref

[Managing environments — conda 4.8.3.post57+fb127b1c documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
