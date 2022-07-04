# WildIris HPC Introductory Tutorial


![](images/WildIris.png)


# Table of contents:

* [Overview](https://github.com/seanharrington256/WildIris_tutorial#Overview)
* [Logging in](https://github.com/seanharrington256/WildIris_tutorial#Logging-in)
	* [OnDemand](https://github.com/seanharrington256/WildIris_tutorial#OnDemand)
* [Navigating WildIris](https://github.com/seanharrington256/WildIris_tutorial#Navigating-WildIris)
* [Moving, copying, and removing (deleting) files](https://github.com/seanharrington256/WildIris_tutorial#Moving-copying-and-removing-files)
* [Editing files](https://github.com/seanharrington256/WildIris_tutorial#Editing-files)
* [Globbing and some useful shortcuts](https://github.com/seanharrington256/WildIris_tutorial#Globbing-and-some-useful-shortcuts)
* [Transferring files
](https://github.com/seanharrington256/WildIris_tutorial#Transferring-files-to-and-from-WildIris)
* [Searching through a file](https://github.com/seanharrington256/WildIris_tutorial#Searching-through-a-file)
* [Compute nodes vs. login nodes](https://github.com/seanharrington256/WildIris_tutorial#Compute-nodes-vs.-login-nodes)
	* [Interactive sessions](https://github.com/seanharrington256/WildIris_tutorial#Interactive-sessions)
	* [Submitting jobs](https://github.com/seanharrington256/WildIris_tutorial#Submitting-jobs)
	* [SLURM](https://github.com/seanharrington256/WildIris_tutorial#SLURM)
* [Modules](https://github.com/seanharrington256/WildIris_tutorial#Modules)
* [Job arrays](https://github.com/seanharrington256/WildIris_tutorial#Job-arrays)




## Overview

This tutorial will walk through the basics of the WildIris high-performance computing (HPC) cluster that is hosted at the University of Wyoming (UW). This cluster is specifically implemented to support users outside of UW and does not require UW credentials/email for access. Hardware for this cluster was purchased with INBRE funds.

If you are looking at this tutorial, then I'm assuming that you already have login credentials that were provided by UW's Advanced Research Computing Center (ARCC -- my sincere apologies for all the acronyms, I hate 'em, too). 

This incorporates some info from Joe's bash tutorial: [https://github.com/Joseph7e/HCGS-BASH-tutorial](https://github.com/Joseph7e/HCGS-BASH-tutorial)



## Logging in

### Secure Shell (SSH)
SSH is a method of securely communicating with another computer.

![alt text](https://www.hostinger.com/tutorials/wp-content/uploads/sites/2/2017/07/symmetric-encryption-ssh-tutorial.jpg)


Logging into WildIris follows the same general procedure as logging into most remote servers. If you are on a Mac or running a Linux operating system, then you can log in directly from the terminal. If you are on a Windows machine, you will need to install an ssh client to allow you to log into and communicate with WildIris, such as [MobaXterm ](https://mobaxterm.mobatek.net/download.html) or [PuTTY](https://www.putty.org/).


Detailed instructions for logging into WildIris are described on ARCC's site [here](https://arccwiki.atlassian.net/wiki/spaces/DOCUMENTAT/pages/1566048281/Connecting+to+WildIris). We'll assume that you've completed your first login. At this point, on a Mac or Linux, you can open a terminal window, type 

`ssh <username>@wildiris.arcc.uwyo.edu`

(where <username> should be replaced by your username on the system)

Then when prompted for a password, enter your password. You will then be asked for a second password: enter the code provided by the FreeOTP app.

This will work basically the same in MobaXterm or PuTTY, but you will put `<username>@wildiris.arcc.uwyo.edu` into the hostname/session window instead of entering it on the command line.

If you've correctly entered your password and FreeOTP code, you should now be logged into WildIris. Keep in mind that as you enter your password, there will be no indication that you've typed anything, you won't see `******` as you might on a website.


### Exiting WildIris

When you are done on WildIris, you can log out with the simple command `exit`.


### OnDemand

You can also access WildIris using OnDemand. This is documented here: [https://arccwiki.atlassian.net/wiki/spaces/DOCUMENTAT/pages/1594163211/WildIris+OnDemand](https://arccwiki.atlassian.net/wiki/spaces/DOCUMENTAT/pages/1594163211/WildIris+OnDemand). We won't use this during the workshop, but it is an alternative that may be helpful if you are having trouble logging in otherwise. It also has cool functionality, including the ability to use RStudio with a graphical interface on WildIris (although I believe that as of the time of writing this on July 4, 2022, that is not yet fully operational).



## Navigating WildIris

The WildIris cluster runs a Linux operating system, as do the vast majority of other HPC clusters. Linux is similar to the Unix-based operating system used on Mac computers. A major difference between using WildIris (and other clusters) and desktop or laptop that is running a Linux or Mac operating sytem is that we have no graphical interface or desktop when we log in to WildIris. Instead, we interact primarily via the command line (for some tools that are exceptions to this, see info about Southpass and Cyberduck below).

This means that we can't just click our way around the cluster to get where we want or see what files and programs are available. Instead, we have to learn some commands that we can use to accomplish these tasks. Commands are entered into the command line in the terminal, and generally share a common structure:

![](images/anatomy.png)

Note that your prompt will look different from mine because I have changed some options in my bash profile (don't worry if that doesn't make much sense to you), and the prompt will look different on different clusters.

One of the most common commands you'll use is 

`ls`

This command lists files and directories. If you run it with no options or arguments, it will do this for the directory you are currently in. 

**Commands are case sensitive!** If you type `LS` it will not be recognized as `ls`. Spaces between options/arguments are also important to delineate when a new option or argument starts. In most cases, the number of spaces is not critical, but it can be for some applications.

When you first log in, you'll be in your home directory, you can always confirm your current directory with the

`pwd`

command (for "print working directory"). This will show you the full path to where you are currently, i.e., all of the nested directories that you are inside of. You should do this often to make sure you're working where you think you are!

If you haven't been using WildIris yet, then you likely won't have any files to see when you run `ls`. We can use `touch` to create a blank text file in our current directory.

```
touch test.txt
```

* Side note: when working in Bash, file extensions are often only used for human convenience and programs will typically not automatically add a file extension. I added `.txt` here so that I know this is a text file (albeit an empty one). We could leave the extension off or use any arbitrary extension and most programs that read text files will still read this file just fine.

Here we have to supply an argument to `touch` to tell it what to name the file. If we run `ls`, we should now see what file listed. I personally prefer to always run `ls` with some additional options as:

`ls -ltrh`

where `l` is long form (includes date information, owner, permissions, and size), `tr` is sort by time, and in reverse (newest files at the bottom), and `h` is human readable so that file sizes are in KB, MB, GB, etc instead of always in bytes.

You can move around on the cluster using `cd` followed by any path (or if you enter `cd` with no path, it will take you to your home directory). If you run

```
cd /
```

It will take you to the root directory of the server. If you run `ls` or `ls -ltrh` here, you'll see all the directories and files that exist in that directory - you won't have permissions to modify most of these and may not be able to even view some.

* **You can return to your home directory by typing `cd`, `cd ~` (the tilde is a shortcut for your home directory), or `cd` followed by the full path to your home directory.** `~` can also be used in paths in other contexts like copying files, designating paths to input files for programs, etc. We'll use it extensively throughout this workshop because everyone has different home directory names, but we can all get to ours by running `cd ~`.

Once back in your home directory, make a new directory called "t3_2022" using the `mkdir` command to make a directory:

```
mkdir t3_2022
```

Then navigate into it:

```
cd t3_2022
```

Note that here we didn't have to use the full path, only what's called the "relative path", meaning we tell the computer where to go relative to where we are already. If we ran that command from somewhere else, it wouldn't work, because the computer doesn't know where to look for `t3_2022`. You can think of this like addresses. If we're in Laramie and I say to go to 108 Grand Ave (Coal Creek Tap), the directions make sense relative to us being in Laramie already. If we're in Ft. Collins, CO, that address doesn't exist, and you need to provide the full address for anyone to be able to get there.

We can navigate up one directory from wherever we are by using `..`

`cd ..`

This can be chained together to move up two or more directories: `cd ../..` goes up two directories, `../../..` goes up three. This can be a bit confusing, so you may want to `pwd` when you finish to know where you are.


Note that if you just want to see what's inside some directory, you can use `ls` without moving into that directory first:


```bash
# List the contents of your home directory
ls ~

# list contents of one directory up from where you are
ls .. 

# list the contents of the root directory
ls /

# list the contents of the t3\_2022 directory you made in your home directory

ls ~/t3_2022
```


## Moving, copying, and removing files

The **move** command - mv

  + mv \<file> \<destination>

The **copy** command - cp

  + cp \<file> \<destination>

The **remove** command - rm

  + rm \<file>

```bash
# make a new directory
mkdir my_directory/

# move a file up one directory
mv my_file.txt ../

# move and rename a file
mv my_file.txt ../my_renamed_file.txt

# copy a file and rename
cp my_file.txt my_renamed_file.txt

# copy a file to a different directory without renaming
cp my_file.txt my_directory/

# remove a file
rm my_renamed_file.txt

# remove a directory with the -r option, recursive
rm -r my_directory/
```


Be **VERY** careful when using `rm`, and even `cp` and `mv`. There is no "undo" button on the command line in Linux and no trashcan. If you delete something with `rm`, it is **gone** and it will not warn you or ask you if you're sure. Similarly, `cp` or `mv` will happily overwrite the target destination with no warning if it already exists.

### Finding help for a command

You can find helpful information about these and most other commands by typing `--help` after the command, e.g., `ls --help` will give you a whole lot of info about using `ls`. Most commands also have great documentation and tutorials that can be found with some quick googling.


## Editing files

We have many options for viewing and editing text files. `nano` is a simple text editor that is available on WildIris and most other Linux and Unix systems. We can test it out on the "test.txt" file we made.

```
nano test.txt
```

Type some text into the file, then run `ctrl + x` to exit (as indicated at the bottom of the editor). It will ask you if you want to save, type `y` for yes, then enter to write to the same file. You could alternately type a different file here to put the modified info into a new file rather than overwriting the old - this is similar to the difference between "save" and "save as" in something like Microsoft Word.

If you are using Cyberduck (described below, getting slightly ahead), you can also edit files using your favorite plain text editor on your local machine. I used [bbedit](https://www.barebones.com/products/bbedit/download.html) on Mac, and used to use [NotePad++](https://notepad-plus-plus.org/downloads/) back when I had a PC. There are plenty of good text editors out there that all mostly do the same thing, these aren't the best, just ones that I started using once and kept using. Once you have one of those (or another) installed, then in Cyberduck, you can right click and go to "edit with", then your preferred editor to open a file on your machine. You can then edit this and save it as usual, and the changes will be saved directly back up to WildIris.

We can also view files (but not edit) using `less`, which is my preferred way of looking inside files:

```
less -S test.txt
```

I almost always use the `-S` options with `less` so that lines stay on a sinle line, rather than wrapping at the end of the screen.


You can also view the start or end of files using `head` or `tail`. If you want to print the entirety of a file to screen, you can use `cat`, but be careful of doing this with large files. If you accidentally do this on a large file and it's taking forever, you can interrupt the current process on the terminal by pressing `control + c`.



## Globbing and some useful shortcuts

Often, we want to select a bunch of files that match some pattern. This can be done with globbing using `*`. The `*` is a wildcard in bash. If we do `ls *.txt` this will list all files that start with anything and end in `.txt`. We can list (or do anything else to) all files with `ls *` - this isn't terrible useful with `ls`, but can be more useful for things like `cp`.

You have probably already noticed that you can't click around the terminal to get to the start or middle of a command that you've started typing. There are a few shortcuts that make it easier to move around if you're at the end of typing some command and need to edit something towards the start before you execute it:

- holding the `control` key and pressing `a` will take you to the start of the prompt
- `ctrl + e` will take you to the end
- `ctrl + u` will delete everything left of your cursor
- `ctrl + k` will delete everything right of your cursor



## Transferring files to and from WildIris

At some point, you will need to upload data from your local computer to WildIris or download data/results from WildIris onto your local computer. There are a few ways to do this. `rsync` and `scp` are both commands that allow you to transfer files over a secure connection. You can find some good scp documentation [here]( https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/) and rsync documentation [here](https://www.digitalocean.com/community/tutorials/how-to-use-rsync-to-sync-local-and-remote-directories#using-rsync-to-sync-with-a-remote-system).


I personally only use these when dealing with really large files or lots of files at a time. Instead, I generally prefer to use the program [Cyberduck](https://cyberduck.io/download/). You also cannot natively use `scp` pr `rsync` on Windows as far as I'm aware so will need Cyberduck or a similar program, like [Filezilla](https://filezilla-project.org/) or [WinSCP](https://winscp.net/eng/index.php).
 
When you open Cyberduck, you should see an "Open Connection button". Click that, select "SFTP" in the dropdown box, enter `wildiris.arcc.uwyo.edu` as the server, then input your username and password. After clicking "connect", you should get a prompt for your second password, which is the code from the FreeOTP app.


![](images/cyberduck_open_cnxn.png)


If you've successfully logged in, you should see a file browser that looks like what you'd see on your desktop. Here you click around through files on WildIris. By default, double clicking a file will download it to your local computer. You can also right click, then select "edit with" to look at a file in any program that will edit it without needing to create a separate copy on your local machine. You can also drag and drop files and directories to and from WildIris using Cyberduck like a regular file browser window on your local machine.

If using Cyberduck, I strongly recommend going into "preferences" (on a Mac this is in the Cyberduck menu left of "File" up top) and in the "transfers" tab select "Use Browser Connection" in the dropdown menu for "Transfer Files". This will prevent Cyberduck from asking for your password every time you upload or download a file.

![](images/cyberduck_browser_cnxn.png)

## Searching through a file

**grep** is a tool that allows you to search through a file for a specified string. With default settings grep will print all lines from a file that contain the exact string that was searched.

```bash

grep "my search string" file.txt

# have a zipped file?
zgrep "my search string" file.txt.gz

# count the number of lines that contain the search string.
grep -c "my search string" file.txt

# diplay the lines that don't contain the search term.
grep -v "my search string" file.txt

```

## Compute nodes vs. login nodes

WildIris is comprised of many individual computers that are all linked together, each of which is called a **node**. Different nodes may have different properties and functions, such as varying numbers of cores (individual processors within a node) and different amounts of memory, you can see an overview of the nodes on WildIris [here](https://arccwiki.atlassian.net/wiki/spaces/DOCUMENTAT/pages/1554972900/WildIris). 

Most important for us most of the time is the distinction between **compute** and **login** nodes. There is a single login node on WildIris. As one might expect, this is the node that you land on when you log in. This node has a limited number of cores and memory, and should only be used for navigating around on the cluster, moving files around, basic text editing, etc. **Do not run computationally intensive processes on the login node**. These will fail or gum up the login node so that other users have a hard time using the cluster.

Instead, anything that is actually processing and analyzing data should be run on a compute node. We'll cover how to do this with interactive sessions and by using slurm job scripts.

### Interactive sessions

Starting an interactive session will move you from the login node onto a compute node, and then everything you enter on the command line will be run on the compute node instead of the login node. You will still enter all of your commands directly into the command line and navigate around as you have been so far. This is done with the `salloc` command.

`salloc` requires that you specify a project with the `-A` option so that usage and priority can be properly monitored. In the T3 2022 workshop, you should all be on the "wy\_t3_2022" project. If you are reading this guide from outside of this workshop, you will need to have use your own project instead. You will likely want to include additional options to specify the amounts of time, memory, and cores to allocate for your session.

This will start an interactive session for 3 hours (format is DAYS-HOURS:MINUTES:SECONDS) with 10 GB of memory and 2 cores.

```bash
salloc -A wy_t3_2022 -t 0-03:00 --mem=10G --cpus-per-task=2
```

Once your session is allocated and running, you can start running commands on the command line with the resources that you requested. If you are done with your session early, you can run `exit` to leave the interactive session and get back to the login node. If you are already on the login node `exit` will terminate your connection to WildIris.

### Submitting jobs

Note that anything you run in an interactive session will terminate if your connection to WildIris is closed. Thus for longer tasks that you don't want to sit and stare at, you can submit a job to WildIris. This is done using a shell script to submit the job to SLURM, the program that schedules jobs on WildIris and many other clusters.

Such scripts start with a header of SLURM options, including how many resources to request, etc.:


```
#!/bin/bash

#SBATCH --job-name FQC   # give the job a name
#SBATCH -A wy_t3_2022    # specify the account
#SBATCH -t 0-04:00		 # how much time?
#SBATCH --nodes=1			# how many nodes?
#SBATCH --cpus-per-task=2	# 2 cores
#SBATCH --mem=10G			# 10 GB memory
#SBATCH --mail-type=ALL		# Send emails on start, fail, completion
#SBATCH --mail-user=USERNAME@gmail.com   # specify your email
#SBATCH -e err_fastqc_%A.err		# name error files and include job ID (%A)
#SBATCH -o std_fastqc_%A.out		# name standard out files and include job ID (%A)
```


A slurm script is just a special kind of shell (bash) script, which is itself just a text file full of bash commands. As mentioned above, file extensions can be arbitrary. Most people us the extension `.sh` to designate shell scripts. I personally use `.slurm` to specifically designate shell scripts that submit slurm jobs - this makes it easy for me to differentiate these from other types of shell scripts and to easily list out my slurm job scripts using `ls *.slurm`

That header is followed by the commands you wish to execute, then you submit a job using `sbatch <your_slurm_script>`.  We'll get deeper into this as we start running jobs in other tutorials, don't worry if this seems really compicated right now.

### SLURM

I've thrown around the term SLURM a few times here, so it's worth stopping for a second to talk about what it is and what it does. SLURM is a scheduler/workload manager for Linu clusters: [https://slurm.schedmd.com/documentation.html](https://slurm.schedmd.com/documentation.html.). What this means for us is that it manages the running of our jobs and decides how many jobs can run at once and when.

This is necessary on a large, multi-user cluster because it's easy for a lot of people with access to all try to run large amounts of large jobs all at once. If everyone could do this freely, then we'd often run into cases where the cluster becomes unusable because there are too many people doing too much at once. When you request an interactive session or submit a job with `sbatch`, SLURM assesses the current load on the system and the amount of resources you've requested and then either allocates your resources and starts your session/job, or puts you in the queue until more resources are available.

* Note that SLURM uses the number of cores and memory that you put in your request to decide whether to run your job. If you massively overestimate the amount of memory required, you may end up queued for a while, whereas a smaller request would've been allocated sooner. Of course the downside is that if you underestimate the required memory, your job may fail.

SLURM also incorporates priority into deciding whose jobs run when. If multiple jobs are queued, it doesn't just run them in order of submission as resources become available. This is helpful because some users will submit thousands of big jobs at a time that could monopolize the cluster for days or weeks if they ran before anyone else's.



## Modules

Modules are pieces or collections of software that are installed on WildIris. There are a lot of programs that are installed and available to users on WildIris. Rather than loading up all of the software each time you log in, users load the individual programs they need as they need them. Some commands for modules:

```
#see a (non-comprehensive) list of available modules
module avail
# search for a specific module and see info on how to load it, here the program bwa
module spider bwa
# load up the bwa module with it's dependcy gcc:
module load gcc/11.2.0 bwa/0.7.17
# See all loaded modules:
module list
# Reset modules to default
module reset
```
* Note that worker nodes do not inherit the loaded modules (or any bash variables, etc.) that are in memory before you start an interactive session or a non-interactive job. You will need to load up modules you need when starting an interactive session or in your SLURM script before the lines that use a given piece of software.


## Job arrays

* We'll come back to this later on after we talk about Bash scripting, but I'm including it here for completeness about working on WildIris.


Loops are very powerful ways to iteratively run the same task over and over: with different settings, with different inputs, with different outputs, there are many ways we can set them up. However, if we make a typical bash loop and execute it within a SLURM script, it will be executed sequentially. That is, if we're doing a task 10 times, it will do the first, then the second, then the third, etc. 

SLURM offers a built in way to effectively loop jobs, where each job runs concurrently (or as many as are allowed at a time by the scheduler and your priority/resources). These are called job arrays.


We execute a job array by adding in an extra line to the `#SBATCH` commands in the header:

```
#SBATCH --array=1-17
```

Will run 17 array jobs. In each job, there will be a bash variable called `$SLURM_ARRAY_TASK_ID` that is the number of the array that is being worked on. We can use this in simple ways to just put that number onto file names or directories. E.g., the following script will make 9 files in a new directory in your home directory, each with the array task ID in the file name:

```
#!/bin/bash

#SBATCH --job-name test_array
#SBATCH -A wy_t3_2022
#SBATCH -t 0-04:00
#SBATCH --nodes=1
#SBATCH --cpus-per-task=2
#SBATCH --mem=10G
#SBATCH --mail-type=ALL
#SBATCH --mail-user=USERNAME@gmail.com
#SBATCH -e err_testarray_%A_%a.err
#SBATCH -o std_testarray_%A_%a.out
#SBATCH --array=1-10

cd ~
mkdir test_array
touch test_array/arraytest$SLURM_ARRAY_TASK_ID.txt
```


Note that we added `%a` to the err and out files to include the task ID in each.

We can get pretty fancy with this to find files and assign them to bash arrays to do the same thing to each file (e.g., say we want to run bwa on a whole bunch of different genomes). We won't get too deep into this, but here is an example of finding all the files we made in the last script, then copying each one to a new file. Rather than feeding these into `cp`, we could feed these or other files into any other program. 



```
#!/bin/bash

#SBATCH --job-name test_array
#SBATCH -A wy_t3_2022
#SBATCH -t 0-04:00
#SBATCH --nodes=1
#SBATCH --cpus-per-task=2
#SBATCH --mem=10G
#SBATCH --mail-type=ALL
#SBATCH --mail-user=USERNAME@gmail.com
#SBATCH -e err_testarray_%A_%a.err
#SBATCH -o std_testarray_%A_%a.out
#SBATCH --array=1-10

cd ~
cd test_array

# use a loop to assign all files starting "arraytest" into a bash array
for x in arraytest*
do
	files=(${files[@]} "${x}")
done


# Use the SLURM_ARRAY_TASK_ID to select a single file out of the bash array
#  I use ($SLURM_ARRAY_TASK_ID-1) because bash indexing starts at 
#     zero and this is easier for me to keep track of.
working_file=${files[($SLURM_ARRAY_TASK_ID-1)]}

cp $working_file COPY_$working_file
```


This will run so fast that it's not really worth doing this way, but it's **EXTREMELY** useful if you're doing lots of repetitive tasks on genomes. I use this to run things like bwa to map dozens of genomes to a reference all at once with a single script rather then making individual scripts for each genome or running them sequentially and waiting forever. I'll even do this for relatively fast things like fastqc if I'm running it on more than a few files at a time.








