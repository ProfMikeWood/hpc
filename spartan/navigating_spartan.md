# Navigating Spartan


## Accessing Spartan from the Command Line

To access Spartan, use the `ssh` command in your terminal with your log in credentials. For example, if you user name is `mike` you will log in with the following command:

```
~ % ssh mike@spartan03.sjsu.edu
```

This prompt will then ask for your password:

```
mwood@spartan03.sjsu.edu's password:
```

Note that you will not see your password as you type - but it will be there.

```{note}
The first time you log in to Spartan, you will provide the default password provided to you with your credentials. Enter your default password and then enter a new password (twice). After completetion, this will log you out of Spartan - simply run the `ssh` command one more time to log back in with your new password.
```

## The Spartan Directory Structure

As is common for HPCs, each user on Spartan is provided with two main directories - a home directory and a "scratch" directory.

### The Home Directory

The home directory on a cluster is the first directory you will land in when you log into the computing cluster. Many users will have a home directory accessed on the same node with shared - and therefore limited - storage. Since storage is limited, your home directory should not be used to store any large files or data. Instead, it should be used to manage configuration files, such as a `.bash_profile`, or perhaps a small installation of `miniconda` in the case that Python or other special software is needed (see more about this on the [conda environment](conda_environments_spartan.md) page). You may also choose to keep a few small files, such as example notes or scripts for loading modules or submitting jobs. 

```{caution}
You should never submit a job from your home directory.
```

### The Scratch Directory

The scratch directory (sometimes called a nobackup directory on other HPCs) is used to store code and data, and submit jobs. On Spartan, if your user nmae is `mike`, your scratch directory is located at

```
/scratch/mike
```

The scratch directories are connected to a larger storage system. In your scratch directory, you are free to upload data and manage codes and files as you see fit. Your scratch directory is yours and can't be edited by other users unless you give them permission.

While there is no strict cap on your storage on Spartan, keep in mind that it is shared across all users. I recommend you keep your storage under approximately 1 TB. If the storage gets too full, the administrators may need to remove some data.

As the same of the directory suggests, the scratch directories are not backed up - so **you should be sure to copy important files to your local machine to ensure you don't lose any crucial data**. 

```{danger}
You should never run computational codes on an HPC without submitting job. Simple tasks are ok - such as moving or zipping files - but all computations should be managed in a job. Read more about submitting jobs on the [Running Jobs on Spartan](running_jobs_spartan.md) page.
```



