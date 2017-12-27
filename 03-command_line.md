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

> > pwd -- shows current working directory path

> > mkdir -- creates a directory
> > rmdir -- removes non-empty directory
> > rm -r -- removes any directory
> > touch filename -- creates a new file
> > rm -- removes a file
> > mv <old_filename> <new_filename> -- renames a file
> > ls -a -- shows all files, including hidden ones
> > ls -d .* -- shows all hidden files
> > ls -d .?* -- shows all hidden files except 1-character files
> > cp <source> <destination> -- copies file from one directory to another

---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls`  
`ls -a`  
`ls -l`  
`ls -lh`  
`ls -lah`  
`ls -t`  
`ls -Glp`  

> > ls -- lists all unhidden files in directory
> > ls -a -- lists all files in directory, including hidden files
> > ls -l -- displays a long listing of files in directory
> > ls -lh -- displays a long listing with file sizes in user-friendly units
> > ls -lah -- displays a long listing of all files, including hidden ones
> > ls -t -- sorts entries by modification time
> > ls -Glp -- displays a long listing with colorized output and slashes after each directory name

---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

> > ls -c -- displays files by filestamp
> > ls -m -- displays names as a comma-separated list
> > ls -R -- displays subdirectories
> > ls -1 -- displays each entry in a separate line
> > ls -r -- displays files in reverse order

---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

> > xargs takes input and executes a chosen command on it, no matter how large the input.
> > Simple example: echo 'one two three' | xargs mkdir take a list of arguments "one two three" and creates three directories named "one", "two", and "three".

 

