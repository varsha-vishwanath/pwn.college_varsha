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
**Flag:** `pwn.college{85fX2r5nRLKqGNDMP5wLvpk00EK.QXwITO0wCM4kjNzEzW}`

I ran cd just to see what would happen, then I got the file path which I used to get the flag.

```
hacker@commands~more-catting-practice:~$ cd
You used 'cd'! In this level, I don't allow you to change the working directory
--- you MUST chase pass 'cat' the absolute path of where I put it on the
filesystem (which is /lib/mysql/private/flag).
hacker@commands~more-catting-practice:~$ cat /lib/mysql/private/flag
pwn.college{85fX2r5nRLKqGNDMP5wLvpk00EK.QXwITO0wCM4kjNzEzW}
```



## Grepping for a Needle in a Haystack
Sometimes, the files that you might cat out are too big. Luckily, we have the grep command to search for the contents we need! We'll learn it in this challenge.

There are many ways to grep, and we'll learn one way here:
```
hacker@dojo:~$ grep SEARCH_STRING /path/to/file
```
Invoked like this, grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

In this challenge, I've put a hundred thousand lines of text into the /challenge/data.txt file. grep it for the flag!

HINT: The flag always starts with the text pwn.college.

## Solve
**Flag:** `pwn.college{wSdO-zPZswoyhzzkCpwr6U2Fxds.QX3EDO0wCM4kjNzEzW}`

```
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{wSdO-zPZswoyhzzkCpwr6U2Fxds.QX3EDO0wCM4kjNzEzW}
```

### New Learnings
I learnt that the grep command basically finds lines of text in a file that has a specific string of text (which is specified in the arguement).



## Comparing Files
When looking for changes between similar files, eyeballing them might not be the most efficient approach! This is where the diff command becomes invaluable.

diff compares two files line by line and shows you exactly what's different between them. For example:
```
hacker@dojo:~$ cat file1
hello
world
hacker@dojo:~$ cat file2
hello
universe
hacker@dojo:~$ diff file1 file2
2c2
< world
---
> universe
```
The output tells us that line 2 changed (2c2), with world in the first file (<) being replaced by universe in the second file (>).

Sometimes, when new lines are added, you'll see something like:
```
hacker@dojo:~$ cat old
pwn
hacker@dojo:~$ cat new
pwn
college
hacker@dojo:~$ diff old new
1a2
> college
```
This tells us that after line 1 in the first file, the second file has an additional line (1a2 means "after line 1 of file1, add line 2 of file2").

Now for your challenge! There are two files in /challenge:

* /challenge/decoys_only.txt contains 100 fake flags
* /challenge/decoys_and_real.txt contains all 100 fake flags plus the one real flag
  
Use diff to find what's different between these files and get your flag!

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


