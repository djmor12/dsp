# Learn command line

Please follow and complete the free online [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. You should be able to go through these in a couple of hours.

**Note:** Bash is not installed on a PC. Rather, PC users must install Cygwin. Once Cygwin has been installed, the command line interface witll _emulate_ bash. You can find all information regarding Cygwin [here](https://www.cygwin.com/).

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

pwd - show current working directory path
mkdir[options]<path> - creating a directory
rm [options] <path> - deleting a directory, use -r if the directory contains other files
touch[options]<path> creating a file using `touch` command
rm <path> -  deleting a file
mv <source path> <new path> - renaming a file
ls -a -  listing hidden files
mv <source path> <new path> - copying a file from one directory to another

---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls`  lists all non-hidden files in current directory
`ls -a`  lists all files in current directory
`ls -l`  displays long list including a file size count, does not include hidden files
`ls -lh`  adds unit suffixs to file size, does not include hiddena files
`ls -lah`  lists all files with file sizes suffixs
`ls -t`   sort by most recently modified to last modified
`ls -Glp`  creates a colorized long list that adds a '/' to a file name if it is a directory

---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

**-F** because it flags file names 
**-c** because it shows files based on timestamp
**-d** because it narrows down the list to directory file names
**-a** because it returns all items in a directory
**-R** returns subdirectories as well

---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

xargs takes the STDIN and executes a command over it.  When combined with the find command, we can search for certain files and execute a command over the specific files using xargs (such as removing or renaming them)
 

