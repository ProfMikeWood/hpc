# Organizing and Moving Files

Once you've got access to Spartan and you've identified your `scratch` directory (as described on the previous page), next you'd probably like to move to items to Spartan. There are two main ways you can move files - `scp` and `rsync`. Use these tools to move any data and files you need onto Spartan in your `scratch` directory.

## Secure Copy Protocol
The `scp` command is used to move files or groups of files between local and remote systems i.e. between your personal computer and Spartan. The `scp` command works the same way as the local `cp` command in that you provide a source path for the files you want to send and a destination path for where the file will end up. The only differnce is that you also need to provide your credentials.

For example, suppose you would like to send a file called `spartan_test.sh` from your computer to your `scratch` directory on Spartan. Assuming you are in the same directory as the file on your local machine, you can run the following command:

```
scp spartan_test.sh mike@spartan03.sjsu.edu:/scratch/mike
```

Note that the path on Spartan is appended to your username and `@spartan03.sjsu.edu`.

Similarly, if you want to move that same file from Spartan to your personal computer, you can reverse the source and destination paths and run the following command (on your personal computer):

```
scp mike@spartan03.sjsu.edu:/scratch/mike/spartan_test.sh Documents
```

This will put the file in your `Documents` folder but you can replace this with any location you would like.

Like the `cp` command, the `scp` has lots of flexibility implemented with various flags. For example, you can the `-r` flag to recursively send a full directory and you can use a wildcard `*` for sending multiple files with the same pattern. 


## Remote Sync

Another extremely useful command for moving files between Spartan and your machine is `rsync`. This command works in a similar way to `scp` except that it can be used to sync one directory with all files it is missing from a separate directory. This can be particularly help if you are moving a lot of data from Spartan to your local drive after you have done a computation - a good habit to get into.

As an example, consider that you want to make a copy of the directory called `Test` in your scratch directory on your local machine. You can use the `rsync` command just like the `scp` command:

```
rsync -av --progress mike@spartan03.sjsu.edu:/scratch/mike/Test/ .
```

Here, we see that we again provide the source path and the destination path (the `.` path mean the present directory). I have also included a few flags here - the `-a` flag stands for `archive` and will preserve file attributes and the `-v` flag mean `verbose` which will print detailed information about the file transfer. I also included a `--progress` flag which will show which files are being transferred.

If new files are added to the Test directory or if the download runs into an error before finishing (e.g. the internet or VPN disconnects), then you can simply run the command one more time. The second time you run the command, you can add the `--ignore-existing` flag as follows, avoiding downloading files you already have:

```
rsync -av --progress --ignore-existing mike@spartan03.sjsu.edu:/scratch/mike/Test/ .
```

```{note}
The trailing slash at the end of the source directory (i.e. after `Test/` in the example above) is important - without this slash, a new folder will be made inside your existing destination folder and the exiting files will not be compared appropriately to the files on the remote system.
```