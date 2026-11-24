# Organizing and Moving Files

Once you've got access to Spartan and you've identified your `scratch` directory (as described on the previous page), next you'd probably like to move to items to Spartan. There are two main ways you can move files - `scp` and `rsync`.

## Secure Copy Protocol
The `scp` command is used to move files or groups of files between local and remote systems i.e. between your personal computer and Spartan. The `scp` command works the same way as the local `cp` command in that you provide a source path for the files you want to send and a destination path for where the file will end up. The only differnce is that you also need to provide your credentials.

For example, suppose you would like to send a file called `test_spartan_job.sh` from your computer to your scratch directory on Spartan. Assuming you are in the same directory as the file you can run the following command on your machine:

```
scp test_spartan_job.txt mike@spartan03.sjsu.edu:/scratch/mwood
```

Note that the path on Spartan is appended to your username and `@spartan03.sjsu.edu`.

Similarly, if you want to move that same file from Spartan to your personal computer, you can reverse the source and destination paths and run the following command (on your personal computer):

```
scp mike@spartan03.sjsu.edu:/scratch/mwood/test_spartan_job.txt Documents
```

This will put the file in your `Documents` folder.

Like the `cp` command, the `scp` has lots of flexibility implemented with various flags. For example, you can the `-r` flag to recursively send a full directory and you can use a wildcard `*` for sending multiple files with the same pattern. 


## Remote Sync

