# Conda Environments on Spartan

When working on Spartan, it's likely that you'll want to use some exterior packages and tools for your project. The Spartan administrators recommend setting this up in a conda environment. This page shows how to create an environment to use some typical Python tools. Although conda environments are often used to manage Python installations, they can also be used for a wide range of modules. See additional examples in the Examples tab for Spartan.

## Creating an Environment

To create a conda envionment called `my-inv` use the Miniforge installation available on Spartan, first ensure you are in your home directory (one of the rare times we will run code in the home directory). Then, use the following series of commands:

```
/opt/Miniforge3/Miniforge3-24.9.0-0-science/bin/conda init bash
conda activate base
conda create -n my-env
conda activate --stack my-env
```

At the end of these script, you should see that your `my-env` environment is activated with the beginning of your terminal line showing this environment in parentheses, i.e. `(my-env) [mike@spartan03 ~]$`.


```{note}
The miniforge version may change from time to time. You can check the most recent version with `ls /opt/Miniforge3`. 
```

## Installing Packages

After you've activated your conda environment, you can install the packages you need into your environment. For example, if you'd like run Python scripts and run calculations with the `numpy` package, you would use the following lines:

```
conda install python=3.12
conda install numpy
```

## Using Your Environment in a Job

conda environments typically need to be activated in order for our scripts to run correctly. However, simply activating your conda environment on the head node does not mean it will be activated on the compute nodes where the job will run. As a result, you'll need to activate your environment in the job script itself. Let's see how this works in an example.

Consider the following python script which we would like to send to the compute nodes:

```{code}
:caption: Contents of python_test.py
import os
import numpy as np

env_name = os.environ.get('CONDA_DEFAULT_ENV', 'Not in a conda environment')
print("Active conda environment: "+env_name)

my_array = np.array([1,2,3,4,5])
print("Example numpy array: "+str(my_array))
```
This is a simple example to show that the conda environment we created is used by the script and that the `numpy` package we installed is working correctly.

As we saw in the previous page about submitting jobs, we will need a job submission script for this code. Let's prepare this as follows:

```
#!/bin/bash
:caption: Contents of test_python.slurm
#SBATCH --partition=nodes
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --time=00:01:00

source /opt/Miniconda3/Miniconda3-py312_24.9.2-0-science/etc/profile.d/conda.sh
conda activate my-env

python python_test.py
```

In the script above, we can see that we call the python script at the end of the job script. However, before we do that we call two lines. The first `source ..../conda/sh` line loads conda's shell integration into the current shell. The second activates our conda environment that we created above. The allows us to have the tools in our conda environment on the compute nodes where our job is run. With this set configuration, we can submit our job as follows:

```
sbatch test_python.slurm
```

If everything has been set up correctly, the output in the `slurm-*.out` file should have the following contents:

```
Active conda environment: my-env
Example numpy array: [1 2 3 4 5]
```

You can use this same approach to install any packages you need for your work in a conda environment. Some examples are shown in the following pages.

