# Pondering Paths

## The root
Alright, so the filesystem starts at /. Under that, there are a whole mess of other directories, configuration files, programs, and, most importantly, flags. In this level, we've added a program right in /, called pwn, that will give you the flag. All you need to do for this level is to invoke this program!

You can invoke a program by providing its path on the command line. In this case, you'll be giving the exact path, starting from /, so the path would be /pwn. This style of path, one that starts with the root directory, is referred to as an "absolute path".

Start the challenge, launch a terminal, invoke the pwn program using its absolute path, and Capture that Flag! Good luck!

### Solve
**Flag:** `pwn.college{AZKRg2zcqV46CA_BsaSHSU_JO87.QX4cTO0wCM4kjNzEzW}`

```
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{AZKRg2zcqV46CA_BsaSHSU_JO87.QX4cTO0wCM4kjNzEzW}
```

### New Learnings
I learned to run a program by its absolute path from the root (/pwn in this case) and that running /pwn runs that exact program no matter where I am or relying on $PATH.
Absolute paths ket you run a specific program directly. 


## Program and Absolute paths
Let's explore a slightly more complicated path! Except for in the previous level, challenges in pwn.college are in the challenge directory and the challenge directory is, in turn, right in the root directory (/). The path to the challenge directory is, thus, /challenge. The name of the challenge program in this level is run, and it lives in the /challenge directory. Thus, the path to the run challenge program is /challenge/run.

This challenge again requires you to execute it by invoking its absolute path. You'll want to execute the run file that is in the challenge directory that is, in turn, in the / directory. If you invoke the challenge correctly, it will give you the flag. Good luck!

### Solve
**Flag:** `pwn.college{AUWcK2CD0p-7E6fLVYPeJxJQ0Hh.QX1QTN0wCM4kjNzEzW}`

type in your solve and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for any bash commands and output you type on the terminal.

```
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{AUWcK2CD0p-7E6fLVYPeJxJQ0Hh.QX1QTN0wCM4kjNzEzW}
```

### New Learnings
I learnt to run a program using its absolute path (/challenge/run), which runs the exact file directly without searching $PATH.



## Position thy self
The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

```
hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
```

This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ~ was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

### Solve
**Flag:** `pwn.college{gCYAdmF1YGl5FgEE3ztGiHGUZ1C.QX2QTN0wCM4kjNzEzW}`

This one took me a second because I didn't know the name of the directory to navigate to using cd. But, after running the previous /challenge/run command first, I was able to find out that I needed to navigate to /var first and completed the challenge.

```
hacker@paths~position-thy-self:~$ cd /challenge/run
bash: cd: /challenge/run: Not a directory
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /var directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-thy-self:~$ cd /var
hacker@paths~position-thy-self:/var$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{gCYAdmF1YGl5FgEE3ztGiHGUZ1C.QX2QTN0wCM4kjNzEzW}
```
### New Learnings
I already knew cd helps navigate between directories, but I now understand that it actually changes the current working directory of the process (in this case, the shell). Programs can depend on this working directory when checking where you are.



## Position elsewhere
The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

```
hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
```

This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ~ was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

### Solve
**Flag:** `pwn.college{4Zw99BN11Cf9Xq3WooKJZxYzCt6.QX3QTN0wCM4kjNzEzW}`

```
hacker@paths~position-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /etc directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-elsewhere:~$ cd /etc
hacker@paths~position-elsewhere:/etc$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{4Zw99BN11Cf9Xq3WooKJZxYzCt6.QX3QTN0wCM4kjNzEzW}
```

### New Learnings
This challenge is pretty much the same as the previous one but I learned that some programs check the shell’s current working directory, so you must cd into the required folder ( /etc) before running the program.



## Position yet elsewhere
The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

```
hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
```

This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ~ was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

### Solve
**Flag:** `pwn.college{o_RGI9w3LW6LaZGdQpNpazRFyqK.QX4QTN0wCM4kjNzEzW}`

```
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the / directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-yet-elsewhere:~$ cd /
hacker@paths~position-yet-elsewhere:/$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{o_RGI9w3LW6LaZGdQpNpazRFyqK.QX4QTN0wCM4kjNzEzW}
```



## Implicit relative paths, from /
Now you're familiar with the concept of referring to absolute paths and changing directories. If you put in absolute paths everywhere, then it really doesn't matter what directory you are in, as you likely found out in the previous three challenges.

However, the current working directory does matter for relative paths.

* A relative path is any path that does not start at root (i.e., it does not start with /).
* A relative path is interpreted relative to your current working directory (cwd).
* Your cwd is the directory that your prompt is currently located at.
  
This means how you specify a particular file, depends on where the terminal prompt is located.

Imagine we want to access some file located at /tmp/a/b/my_file.

* If my cwd is /, then a relative path to the file is tmp/a/b/my_file.
* If my cwd is /tmp, then a relative path to the file is a/b/my_file.
* If my cwd is /tmp/a/b/c, then a relative path to the file is ../my_file. The .. refers to the parent directory.
  
Let's try it here! You'll need to run /challenge/run using a relative path while having a current working directory of /. For this level, I'll give you a hint. Your relative path starts with the letter c 😊

### Solve
**Flag:** `pwn.college{gcdu9piw3eZt34a1tgR9EylvN5h.QX5QTN0wCM4kjNzEzW}`

```
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{gcdu9piw3eZt34a1tgR9EylvN5h.QX5QTN0wCM4kjNzEzW}
```

### New Learnings
This challenge taught me how relative paths work: they don’t start with / (they don't start from the root) and are found within the shell’s current working directory (cwd). By navigating to / and then running challenge/run, I invoked /challenge/run using a relative path and got the flag.



## Explicit relative paths, from /
Previously, your relative path was "naked": it directly specified the directory to descend into from the current directory. In this level, we're going to explore more explicit relative paths.

In most operating systems, including Linux, every directory has two implicit entries that you can reference in paths: . and ... The first, ., refers right to the same directory, so the following absolute paths are all identical to each other:

* /challenge
* /challenge/.
* /challenge/./././././././././
* /./././challenge/././
  
The following relative paths are also all identical to each other:

* challenge
* ./challenge
* ./././challenge
* challenge/.
  
Of course, if your current working directory is /, the above relative paths are equivalent to the above absolute paths.

This challenge will get you using . in your relative paths. Get ready!

### Solve
**Flag:** `pwn.college{AuqZH9GiMptSTay1VzWJsJPk0oC.QXwUTN0wCM4kjNzEzW}`

```
hacker@paths~explicit-relative-paths-from-:~$ /challenge/run
Incorrect...
You are not currently in the / directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~explicit-relative-paths-from-:~$ cd /
hacker@paths~explicit-relative-paths-from-:/$ challenge/run
Incorrect...
This challenge must be called with a relative path that explicitly starts with a `.`!
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{AuqZH9GiMptSTay1VzWJsJPk0oC.QXwUTN0wCM4kjNzEzW}
```

### New Learnings
I learned that . is a shortcut for the current directory. I was initially confused by this challenge, not because it was difficult, but because I didn’t understand why using . mattered compared to just a relative path. After looking it up, I understand that . is used for safety and organization: it explicitly runs the program in the cwd, which is predictable and avoids accidentally running a program elsewhere. This is especially important if . is not included in $PATH. I also learned that .. refers to the parent directory which one level above the cwd.

### References 
https://superuser.com/questions/153165/what-does-represent-while-giving-path#:~:text=.%2F%20does%20not%20begin,working%20directory.&text=Thus%2C%20we%20need%20to,working%20directory.&text=case%2C%20the%20operation%20is,working%20directory.&text=the%20current%20directory%2C%20if,working%20directory.
