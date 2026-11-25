# Running jobs on Spartan

High performance computing clusters implement a job queue to manage computations submitted by different users. Spartan uses a commonly-used job manager called **slurm**. Here, we'll walk through the steps to create a job submission script and submit the job to Spartan in the slurm system.

## An Example Job
To showcase the steps to submit a job on Spartan, we'll use an example script called `spartan_test.sh` which prints out a line, pauses for 30 seconds, and then prints out another line:

```{code} python
:caption: Contents of `spartan_test.sh`

echo "The script has started, sleeping for 30 seconds"
sleep 30
echo "Waking back up, script has ended"
```

We will send this script to run on the compute nodes using a slurm job script.

## Creating a Job Script
A job script outlines the time and resources required to run the job as well as other pertinent parameters.

### Job Script Format
A job script has three components:
1. Header lines passed to the job management system (slurm)
2. Pertinent set-up checks (e.g. purging/loading modules, checking files structures)
3. Running the job executable(s)


### Example slurm job script for `spartan_test.sh`

The following code shows an example job submission script called `test_job.slurm` for the `spartan_test.sh` code we wrote above:

```{code}
:caption: Contents of `test_job.slurm`

#!/bin/bash
#SBATCH --partition=nodes
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --time=00:01:00
#SBATCH --mail-user=first.last@email.com
#SBATCH --mail-type=ALL

bash spartan_test.sh
```

#### The slurm header
In the script above, we can see that there are several lines beginning with `#SBATCH` - these lines pass information to the job scheduler which explain how the job should be handled. The purpose of these lines are summarized in the following table:

| Line | Purpose |
|---------|---------|
|#SBATCH --partition=nodes | This line passes the job to the `nodes` partition of Spartan. The `nodes` partition has 72 Broadwell nodes with 28 CPUs each. Unless your code is set up to run on GPUs, this will be your default partition. |
|#SBATCH --nodes=1| This line requests to use one node. Unless your code is designed to run in parallel across multiple nodes, this number should be 1. |
|#SBATCH --ntasks=1| This line requests to use one CPU. Again, unless your code is designed to run in parallel across multiple CPUs, this number should be 1. Note also that "multithredding" on a single CPU is different from running accross multiple CPUs. |
|#SBATCH --time=00:01:00| This line requests one minute of computational time for your script. You job script should included an estimated allotment of time for your script to run with some buffer time for good measure. |
|#SBATCH --mail-user=first.last@email.com | This line will send an email to you with updates about your job. This can be helpful when running long jobs so you don't need to monitor them all of the time. However, it is not necessary to include.
|#SBATCH --mail-type=ALL| This line describes what should be sent to you via email. Be default, it will include emails for both the starting of your script and the ending of your script. Again, it is not necessary to include. |

#### The job script body
The body of the job script, under the slurm header, will include all of the code that will be run on the compute nodes. This should include any prerequisites for your scripts, such as modules and conda environments, as well as the script itself. In the example above, the body is very simple - its just the line required to run the script: `bash spartan_test.sh`.

## Submitting a Job

Once you've got your job script prepared, your ready to run your job. From the directory where your submission script (e.g. `test_job.slurm`) and your job script (e.g. `spartan_test.sh`) are located, run the following command:

```
sbatch test_job.slurm
```

The code above will send your job to the compute nodes.

### Checking on your job

To check the on the status of your job use the `squeue -u` command along with your user name, e.g.: 

```{code}
[mike@spartan03 Test]$ squeue -u mike
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
            620185     nodes test_job     mike  R       0:19      1 node17
```

In this output, we can see the following information about the job:
- the job ID name (620185)
- the parition (nodes)
- the user name (mike)
- the job status (R = Running)
- the total time elapsed (0:19)
- the number of nodes in use by the user (1)
- the name of the node where the job is running (node17)

If the user wanted to cancel the job due to an error noticed in the output, they could run
```
scancel 620185
```

## Assessing a job when its complete

When a job is complete, the job management system will provide a file that contains all of the output and some summative information on the run.

On slurm, the file will be named `slurm-[jobID].out`. For the example given above, this would be `slurm-620185.out`. You can check the contents of this file using your favorite command line text editor (e.g. nano or vim) or you can dump the outputs with the `cat` command. If we run this on the script above:

```
cat slurm-620185.out
```

We see the following output:
```
The script has started, sleeping for 30 seconds
Waking back up, script has ended
```

Of course, this is the output our code was designed to produce.


## Common slurm Commands

The table below summarizes the common slurm commands introduced above:
| Action | slurm |
| ---------- |----------- |
| Submit a job script | sbatch script_name |
| Check jobs currently in the queue | squeue |
| Check jobs currently in the queue for a given user | squeue -u user |
| Cancel a job with ID job_id | scancel job_id |

