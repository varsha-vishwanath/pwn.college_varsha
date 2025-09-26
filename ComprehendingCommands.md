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
**Flag:** `pwn.college{M-ic5gAIIaSSNj_wsL33KZnLSEk.01MwMDOxwCM4kjNzEzW}`

```
hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
9a10
> pwn.college{M-ic5gAIIaSSNj_wsL33KZnLSEk.01MwMDOxwCM4kjNzEzW}
```

The output here tells us that after line 9 of decoys_only.txt, another line was added to get decoys_and_real.txt. This line was the flag

### New Learnings
I learnt that diff is an efficient way to find differences between two files. By running diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt I could see exactly which line was added in the second file instead of manually scanning 100 lines.



## Listing Files
So far, we've told you which files to interact with. But directories can have lots of files (and other directories) inside them, and we won't always be here to tell you their names. You'll need to learn to list their contents using the ls command!

ls will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided. Observe:
```
hacker@dojo:~$ ls /challenge
run
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$
```
In this challenge, we've named /challenge/run with some random name! List the files in /challenge to find it.

## Solve
**Flag:** `pwn.college{QX8RdKz-EbGzhmC1MEDh4wuhGmc.QX4IDO0wCM4kjNzEzW}`

```
hacker@commands~listing-files:~$ ls /challenge
4684-renamed-run-21769  DESCRIPTION.md
hacker@commands~listing-files:~$ /challenge/4684-renamed-run-21769
Yahaha, you found me! Here is your flag:
pwn.college{QX8RdKz-EbGzhmC1MEDh4wuhGmc.QX4IDO0wCM4kjNzEzW}
```

### New Learnings
I learned that ls lists a directory’s contents and is the first tool to use when a file name isn’t given. By running ls /challenge I discovered the renamed binary 4684-renamed-run-21769 and executed it with its absolute path to get the flag.



## Touching Files
Of course, you can also create files! There are several ways to do this, but we'll look at a simple command here. You can create a new, blank file by touching it with the touch command:
```
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ touch pwnfile
hacker@dojo:/tmp$ ls
pwnfile
hacker@dojo:/tmp$
```
It's that simple! In this level, please create two files: /tmp/pwn and /tmp/college, and run /challenge/run to get your flag!

## Solve
**Flag:** `pwn.college{gd_HwrSN5pgJ8AkVfK8UB21lJS3.QXwMDO0wCM4kjNzEzW}`

```
hacker@commands~touching-files:~$ cd /tmp
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ ls
bin  hsperfdata_root  pwn  tmp.TpSOPGOVKK
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$ ls
bin  college  hsperfdata_root  pwn  tmp.TpSOPGOVKK
hacker@commands~touching-files:/tmp$ /challenge/run
Success! Here is your flag:
pwn.college{gd_HwrSN5pgJ8AkVfK8UB21lJS3.QXwMDO0wCM4kjNzEzW}
```

### New Learnings
I learned how to create files with the touch command. touch pwn and touch college created the required empty files in /tmp, and the challenge binary then detected their presence and printed the flag. I also practiced verifying files with ls.

## Removing Files
Files are all around you. Like candy wrappers, there'll eventually be too many of them. In this level, we'll learn to clean up!

In Linux, you remove files with the rm command, as so:
```
hacker@dojo:~$ touch PWN
hacker@dojo:~$ touch COLLEGE
hacker@dojo:~$ ls
COLLEGE     PWN
hacker@dojo:~$ rm PWN
hacker@dojo:~$ ls
COLLEGE
hacker@dojo:~$
```
Let's practice. This challenge will create a delete_me file in your home directory! Delete it, then run /challenge/check, which will make sure you've deleted it and then give you the flag!

### Solve
**Flag:** `pwn.college{8BYtf29tpPlhNAZTLE8FLWMaNzh.QX2kDM1wCM4kjNzEzW}`

```
hacker@commands~removing-files:~$ ls
a  delete_me
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ ls
a
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{8BYtf29tpPlhNAZTLE8FLWMaNzh.QX2kDM1wCM4kjNzEzW}
```

### New Learnings
I learned how to use the rm command to delete files. By removing delete_me from my home directory, I satisfied the program’s check, which then rewarded me with the flag. I also reinforced the habit of verifying deletions with ls before and after using rm.



## Moving Files
You can also move files around with the mv command. The usage is simple:
```
hacker@dojo:~$ ls
my-file
hacker@dojo:~$ cat my-file
PWN!
hacker@dojo:~$ mv my-file your-file
hacker@dojo:~$ ls
your-file
hacker@dojo:~$ cat your-file
PWN!
hacker@dojo:~$
```
This challenge wants you to move the /flag file into /tmp/hack-the-planet (do it)! When you're done, run /challenge/check, which will check things out and give the flag to you.

### Solve
**Flag:** `pwn.college{oqwUGbmPf9-5DgZgm_mwoAlgdIH.0VOxEzNxwCM4kjNzEzW}`

```
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{oqwUGbmPf9-5DgZgm_mwoAlgdIH.0VOxEzNxwCM4kjNzEzW}
```

### New Learnings
I learned that the mv command can be used to both rename and move files and directories. If the arguement of the mv command is old_name new_name (as shown in the example), mv renames it. If the arguement is file_name new/file/path (as given in the challenge) then mv moves it as needed.

### References
https://www.w3schools.com/bash/bash_mv.php



## Hidden files
