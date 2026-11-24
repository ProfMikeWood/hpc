# MITgcm on Spartan


This page gives an example for how to run MITgcm on Spartan.


## Creating a conda environment with tools for MITgcm

Begin by making a conda environment for MITgcm

```
/opt/Miniforge3/Miniforge3-24.9.0-0-science/bin/conda init bash
conda activate base
conda create -n mitgcm
conda activate --stack mitgcm
```

Then, install the following packages:

```
conda install gcc=9.5.0 netcdf4 mpich hdf5 -c conda-forge
```

