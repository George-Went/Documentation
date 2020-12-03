# Shell Scripts 

## What is a shell 
A shell provides a interface/environment to the unix system.
It gathers inputted data ( usually in the form of a command line) and excecutes the program based on the inputs

The most commonly used shell in unix systems is BASH (Bourne Shell), if you use a terminal to interact with a linux system you will have used bash. All bash commands start with `$`.

when you enter in a command to linux such as `ls` you are executing a single line bash script to interact with the unix operating system (the `$` is automatically added at the start in the terminal).

## Common Commands on Linux
If you've used a terminal on a linux system you will have had experance in using bash. Here are some of the most common commands.

`pwd`: Find out the directory you are in.
`cd`: Change directories
`ls`: list contents of a directory
`cat`: short for conacatonate. List the standard output (`echo and teminal responses) and also join files together.
`cp`: copy files
`mkdir`: move files
`chomd`: change read, write and execute permission of files.


## Creating and Executing Simple Scripts
We can write simple scripts on the terminal command line.
To start off with, we can write 
```bash
$echo Hello World
```
When run (by pressing enter) the terminal will print out `Hello World`.

We can also save bash scripts as files, rather than executing them right after we write them. We can then just call the file name to execute the script. we can store bash scripts with the `.sh` filetype to denaote that they are bash scripts. (Note that in linux, the `/sh` is not needed and is only ther for the user to understand what the file is)

helloWolrd.sh
```bash
#!/bin/bash
echo "what is your name?"
read name 
echo "$name"
```

## Permissions and chmod 
Before we can run the bash script, we have to change the *permissions* of the file tpye. Normally on a computer, a file has to have permissions to operate - you dont want a file in a downloads fodler to be able to change your root filesystem. 

If you run `ls -l` on the above `helloWorld.sh` file you can see that we get:  
```
-rw-rw-r-- 1 username username 61 Oct  6 11:47 HelloWorld.sh
```


The first part is what we are looking for with permissions: `-rw-rw-r--`
This means that the owner and the group he is in can read and write the file, but cannot execute it.

```
-rw-r--r-- 12 username users 12.0K Apr  8 20:51 filename.txt
|[-][-][-]-   [------] [---]
| |  |  | |      |       |
| |  |  | |      |       +-----------> 7. Group
| |  |  | |      +-------------------> 6. Owner
| |  |  | +--------------------------> 5. Alternate Access Method
| |  |  +----------------------------> 4. Others Permissions
| |  +-------------------------------> 3. Group Permissions
| +----------------------------------> 2. Owner Permissions
+------------------------------------> 1. File Type
```

We can chaneg ther permissions in a variety of ways using `chmod`. One of the best examples of a chmod command is `chmod +x`, which changes a files permissions so that it is executable:

helloWorld afert `chmod +x helloWolrd` is run:
```
-rwxrwxr-x 1 username user 61 Oct  6 11:47 HelloWorld.sh
```
This means we can now execute the file.




ss