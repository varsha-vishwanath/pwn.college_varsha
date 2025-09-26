	# Comprehending Commands

## cat: not the pet, but the command!
One of the most critical Linux commands is cat. cat is most often used for reading out files, like so:
```
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
One of the most critical Linux commands is `cat`.
```
`cat` is most often used for reading out files, like so:
cat will concatenate (hence the name) multiple files if provided multiple arguments. For example:
```
hacker@dojo:~$ cat myfile
This is my file!
hacker@dojo:~$ cat yourfile
This is your file!
hacker@dojo:~$ cat myfile yourfile
This is my file!
This is your file!
hacker@dojo:~$ cat myfile yourfile myfile
This is my file!
This is your file!
This is my file!
```
Finally, if you give no arguments at all, cat will read from the terminal input and output it. We'll explore that in later challenges...

In this challenge, I will copy the flag to the flag file in your home directory (where your shell starts). Go read it with cat!

### Solve
**Flag:** `pwn.college{Q5GE4oINfou5KUh95ZlUJ9wALdi.QXxcTN0wCM4kjNzEzW}`

I incorrectly assumed that the file would be file.md but once I replaced it with a generic file name (as given in the example) I was able to find the flag.

```
hacker@commands~cat-not-the-pet-but-the-command:~$ cat ~/flag.md
cat: /home/hacker/flag.md: No such file or directory
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{Q5GE4oINfou5KUh95ZlUJ9wALdi.QXxcTN0wCM4kjNzEzW}
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag flag
pwn.college{Q5GE4oINfou5KUh95ZlUJ9wALdi.QXxcTN0wCM4kjNzEzW}
pwn.college{Q5GE4oINfou5KUh95ZlUJ9wALdi.QXxcTN0wCM4kjNzEzW}
```

### New Learnings
I learnt that cat is a command that returns the contents of a specified file and that it can be run with multiple arguements that would be concatenated. Additionally, if cat is run with no arguements, it will read from the terminal input. 
So it will echo the input from the keyboard until it is terminated. 



## Catting Absolute Paths
In the last level, you did cat flag to read the flag out of your home directory! You can, of course, specify cat's arguments as absolute paths:
```
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
In the last level, you did `cat flag` to read the flag out of your home directory!
You can, of course, specify `cat`'s arguments as absolute paths:
...
```
In this directory, I will not copy it to your home directory, but I will make it readable. You can read it with cat at its absolute path: /flag.

FUN FACT: /flag is where the flag always lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.

### Solve
**Flag:** `pwn.college{Ex9NKeoLyzmJo6dJpmmv-lUB3BN.QX5ETO0wCM4kjNzEzW}`

```
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{Ex9NKeoLyzmJo6dJpmmv-lUB3BN.QX5ETO0wCM4kjNzEzW}
```

### New Learnings
I learned that cat can also have an absolute path as its arguement.



## More Catting Practice
You can specify all sorts of paths as arguments to commands, and we'll practice some more with cat. In this level, I'll put the flag in some crazy directory, and I will not allow you to change directories with cd, so no cat flag for you. You must retrieve the flag by absolute path, wherever it is.

### Solve
**Flag:** `pwn.college{helloworld}`

type in your solve and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for any bash commands and output you type on the terminal.

```bash
command 1
command 2
pwn.college{helloworld}
```

### New Learnings
Brief note on what you learned from the challenge

### References 
Add any references or videos you used while solving the challenge.


