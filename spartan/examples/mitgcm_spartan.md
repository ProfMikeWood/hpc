# MITgcm on Spartan


This page gives an example for how to install and run the MIT General Circulation Model (MITgcm) on Spartan. MITgcm is a common model used in oceanographic studies. Information on MITgcm can be found on the model ReadTheDocs page here: https://mitgcm.readthedocs.io/en/latest/. Information about how to build an MITgcm model and run it on a computing cluster can be found on my notes here: https://profmikewood.github.io/ocean_modeling_book/intro.html. This page details the set up for Spartan in particular.


## Installing MITgcm

MITgcm is "installed" by cloning a the Github repository for the latest model release. Change directories to your scratch directory and clone the Github repostitory:

```
cd /scratch/mike
git clone https://github.com/MITgcm/MITgcm.git
```

## Creating a conda environment with tools for MITgcm

To compile the code for an MITgcm model configuration, we'll need a Fortran compiler and associated tools for parallelizing code with MPI and storing netCDF files. These tools can all be installed in a conda environment. Similar tohe Python example shown on the [conda environments page](../conda_environments_spartan.md), we can create an environment named `mitgcm` as follows:

```
/opt/Miniforge3/Miniforge3-24.9.0-0-science/bin/conda init bash
conda activate base
conda create -n mitgcm
conda activate --stack mitgcm
```

Then, we can install the necessary packages with this line:

```
conda install gcc=9.5.0 netcdf4 mpich hdf5 -c conda-forge
```

## Compiling code for MITgcm
The compilation of MITgcm code will require the both the compiler and the MPI installation installed above. To compile code in MITgcm, be sure that your `mitgcm` conda environment is activation. Then, ensure you have an environment variable that points to the location of MPI in your conda environment. You can add the following line to your build script:

```{code}
export MPI_HOME=/home/mike/.conda/envs/mitgcm
```

Obviously, you should update your user name and the name of your conda environment (if it is not called `mitgcm`).

In total, a complete compilation should look as follows:

```{code}
:caption: Example build script for compiling code on Spartan
cd build
export MPI_HOME=/home/mike/.conda/envs/mitgcm
../../../tools/genmake2 -of ../../../tools/build_options/linux_amd64_gfortran -mods ../code -mpi
make depend
make
```

Note that the relative paths above assume you are in a folder such as:

```
/scratch/mike/MITgcm/configurations/my_model
```


## Running an MITgcm model configuration on Spartan

Once you've successfully compiled your code and you obtain the `mitgcmuv` executable for your code, you're ready to run. As for all computations on the computing cluster, we will need to make a job script. Inside the `run` directory for your model, your script should look as follows:

```{code}
:caption: Example job submission script for running MITgcm on Spartan
#!/bin/bash
#SBATCH --partition=nodes
#SBATCH --nodes=3
#SBATCH --ntasks=72
#SBATCH --time=120:00:00

export MPI_HOME=/home/mike/.conda/envs/mitgcm
mpirun -np 72 ./mitgcmuv
```

It is important to note here that the number of CPUs request (72 CPUs divided across 3 nodes) is equal to the number of processors requested for the run when running the executable with MPI. This is explained in the next section.

### Determining the number of CPUs and Nodes
When requesting resources for our model, we need to determine how many CPUs are required for the job. In the case of MITgcm, the number of CPUs is the total number of processors identified in the `SIZE.h` file (`nPx`*`nPy`). After the CPUs have been determined, next you need to determine the nodes to request for the job - the key component of the job script. The number of nodes for a job is determined by how many CPUs are on each node, On Spartan, each node contains 2 Broadwell processors containing 14 CPUs, resulting in 28 CPUs per node. Thus, the total nodes required for your job is given by

$
\text{nodes} = \text{ceiling}\left(\frac{\text{nunber of cpus}}{\text{cpus per node}}\right)
$

#### Model example

For the model above, the `SIZE.h` file has the following partitioning:

```
     &           nPx =   6,
     &           nPy =   12,
```

This means that the job will need 72 CPUs to run. From the formula above, we see that 

$
\text{nodes} = \text{ceiling}\left(\frac{72}{28}\right) = 3
$

Hence, in the job submission script above, we request:

```{code}
#SBATCH --nodes=3
```