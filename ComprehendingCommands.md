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
Interestingly, ls doesn't list all the files by default. Linux has a convention where files that start with a . don't show up by default in ls and in a few other contexts. To view them with ls, you need to invoke ls with the -a flag, as so:
```
hacker@dojo:~$ touch pwn
hacker@dojo:~$ touch .college
hacker@dojo:~$ ls
pwn
hacker@dojo:~$ ls -a
.college	pwn
hacker@dojo:~$
```
Now, it's your turn! Go find the flag, hidden as a dot-prepended file in /.

### Solve
**Flag:** `pwn.college{AEExBpBjO0YKEMLHex95wQhcnXr.QXwUDO0wCM4kjNzEzW}`

```
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv             bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-213582595411953  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ cat /.flag-213582595411953
pwn.college{AEExBpBjO0YKEMLHex95wQhcnXr.QXwUDO0wCM4kjNzEzW}
```

### New Learnings
I learned that Linux treats files starting with . as hidden. ls won’t display them unless you use ls -a. 
. is primarily used to hide configuration files in a home directory in order to keep the directory clean looking

### References
https://superuser.com/questions/628884/why-will-ls-not-list-files-starting-with-in-linux



## An Epic Filesystem QuestWith your knowledge of cd, ls, and cat, we're ready to play a little game!

We'll start it out in /. Normally:
```
hacker@dojo:~$ cd /
hacker@dojo:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  dev        flag  lib   lib64  media   opt  root  sbin  sys  usr
```
That's a lot of contents! One day, you will be quite familiar with them, but already, you might recognize the flag file and the challenge directory.

In this challenge, I have hidden the flag! Here, you will use ls and cat to follow my breadcrumbs and find it! Here's how it'll work:

0. Your first clue is in /. Head on over there.
1. Look around with ls. There'll be a file named HINT or CLUE or something along those lines!
2. cat that file to read the clue!
3. Depending on what the clue says, head on over to the next directory (or don't!).
4. Follow the clues to the flag!
   
Good luck!

### Solve
**Flag:** `pwn.college{Ir_PCDKOyLn3A5YVL-xUArj-haY.QX5IDO0wCM4kjNzEzW}`

```bash
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls -a
.   .dockerenv  bin   challenge  etc   home  lib32  libx32  mnt  opt   root  sbin  sys  usr
..  REVELATION  boot  dev        flag  lib   lib64  media   nix  proc  run   srv   tmp  var
hacker@commands~an-epic-filesystem-quest:/$ cat REVELATION
Lucky listing!
The next clue is in: /usr/lib/python3/dist-packages/binwalk/__pycache__

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/$ cd  /usr/lib/python3/dist-packages/binwalk/__pycache__
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/binwalk/__pycache__$ ls -a
.  ..  MESSAGE  __init__.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/binwalk/__pycache__$ cat MESSAGE
Congratulations, you found the clue!
The next clue is in: /usr/lib/python3.8/xml/etree/__pycache__

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/binwalk/__pycache__$ cd /usr/lib/python3.8/xml/etree/__pycache__
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3.8/xml/etree/__pycache__$ ls -a
.   .SPOILER                       ElementPath.cpython-38.pyc  __init__.cpython-38.pyc
..  ElementInclude.cpython-38.pyc  ElementTree.cpython-38.pyc  cElementTree.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3.8/xml/etree/__pycache__$ cat.SPOILER
bash: cat.SPOILER: command not found
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3.8/xml/etree/__pycache__$ cat .SPOILER
Great sleuthing!
The next clue is in: /usr/lib/python3/dist-packages/future/backports/test
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3.8/xml/etree/__pycache__$ cd /usr/lib/python3/dist-packages/future/backports/test
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/future/backports/test$ ls -a
.     __init__.py  badkey.pem                     keycert.passwd.pem  nokia.pem         pystone.py    ssl_key.passwd.pem  support.py
..    __pycache__  dh512.pem                      keycert.pem         nullbytecert.pem  sha256.pem    ssl_key.pem
NOTE  badcert.pem  https_svn_python_org_root.pem  keycert2.pem        nullcert.pem      ssl_cert.pem  ssl_servers.py
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/future/backports/test$ cat NOTE
Tubular find!
The next clue is in: /usr/local/lib/python3.8/dist-packages/packaging-25.0.dist-info/licenses

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/future/backports/test$ cd /usr/local/lib/python3.8/dist-packages/packaging-25.0.dist-info/licenses
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/packaging-25.0.dist-info/licenses$ ls -a
.  ..  LICENSE  LICENSE.APACHE  LICENSE.BSD  NUGGET
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/packaging-25.0.dist-info/licenses$ cat NUGGET
Lucky listing!
The next clue is in: /usr/share/doc/libargon2-1
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/packaging-25.0.dist-info/licenses$ cd /usr/share/doc/libargon2-1
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libargon2-1$ ls -a
.  ..  SNIPPET  changelog.Debian.gz  copyright
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libargon2-1$ cat SNIPPET
Yahaha, you found me!
The next clue is in: /opt/linux/linux-5.4/lib/842
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libargon2-1$ cd /opt/linux/linux-5.4/lib/842
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/lib/842$ ls -a
.  ..  842.h  842_compress.c  842_debugfs.h  842_decompress.c  Makefile  POINTER
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/lib/842$ cat POINTER
Lucky listing!
The next clue is in: /usr/share/icons/LoginIcons/apps/64

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/lib/842$ ls -a /usr/share/icons/LoginIcons/apps/64
.  ..  INFO-TRAPPED  computer.svg
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/lib/842$ cat /usr/share/icons/LoginIcons/apps/64/INFO-TRAPPED
Yahaha, you found me!
The next clue is in: /usr/share/doc/libgbm1

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/lib/842$ ls -a /usr/share/doc/libgbm1
.  ..  .TEASER  changelog.Debian.gz  copyright
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/lib/842$ cat  /usr/share/doc/libgbm1/TEASER
cat: /usr/share/doc/libgbm1/TEASER: No such file or directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/lib/842$ cat /usr/share/doc/libgbm1/TEASER
cat: /usr/share/doc/libgbm1/TEASER: No such file or directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/lib/842$ cat /usr/share/doc/libgbm1/.TEASER
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{Ir_PCDKOyLn3A5YVL-xUArj-haY.QX5IDO0wCM4kjNzEzW}
```

### New Learnings
I learned how to follow breadcrumbs through the filesystem using cd, ls, and cat. I learned to handle delayed clues that only become readable after entering a directory, as well as hidden files starting with a . that require ls -a to view. I also practiced reading files without changing directories, which is useful for safely accessing “trapped” files. Overall, it strengthened my understanding of navigating Linux directories, finding files, and combining commands to extract information efficiently.



## Making Directories
We can create files. How about directories? You make directories using the mkdir command. Then you can stick files in there!

Watch:
```
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ mkdir my_directory
hacker@dojo:/tmp$ ls
my_directory
hacker@dojo:/tmp$ cd my_directory
hacker@dojo:/tmp/my_directory$ touch my_file
hacker@dojo:/tmp/my_directory$ ls
my_file
hacker@dojo:/tmp/my_directory$ ls /tmp/my_directory/my_file
/tmp/my_directory/my_file
hacker@dojo:/tmp/my_directory$
```
Now, go forth and create a /tmp/pwn directory and make a college file in it! Then run /challenge/run, which will check your solution and give you the flag!

### Solve
**Flag:** `pwn.college{Meg2cv-KM6oafkS9Opd5-T8Iz1S.QXxMDO0wCM4kjNzEzW}`

```
hacker@commands~making-directories:~$ cd /tmp
hacker@commands~making-directories:/tmp$ mkdir pwn
hacker@commands~making-directories:/tmp$ ls
bin  hsperfdata_root  pwn  tmp.4mK6TfTSUV
hacker@commands~making-directories:/tmp$ cd pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ ls
college
hacker@commands~making-directories:/tmp/pwn$ /challenge/run
Success! Here is your flag:
pwn.college{Meg2cv-KM6oafkS9Opd5-T8Iz1S.QXxMDO0wCM4kjNzEzW}
```

### New Learnings
I learned how to use mkdir to create directories and touch to create files inside them. By making /tmp/pwn and adding an empty college file, I satisfied the program’s expectations and received the flag.



## Finding Files
So now we know how to list, read, and create files. But how do we find them? We use the find command!

The find command takes optional arguments describing the search criteria and the search location. If you don't specify a search criteria, find matches every file. If you don't specify a search location, find uses the current working directory (.). For example:
```
hacker@dojo:~$ mkdir my_directory
hacker@dojo:~$ mkdir my_directory/my_subdirectory
hacker@dojo:~$ touch my_directory/my_file
hacker@dojo:~$ touch my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find
.
./my_directory
./my_directory/my_subdirectory
./my_directory/my_subdirectory/my_subfile
./my_directory/my_file
hacker@dojo:~$
```
And when specifying the search location:
```
hacker@dojo:~$ find my_directory/my_subdirectory
my_directory/my_subdirectory
my_directory/my_subdirectory/my_subfile
hacker@dojo:~$
```
And, of course, we can specify the criteria! For example, here, we filter by name:
```
hacker@dojo:~$ find -name my_subfile
./my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find -name my_subdirectory
./my_directory/my_subdirectory
hacker@dojo:~$
```
You can search the whole filesystem if you want!
```
hacker@dojo:~$ find / -name hacker
/home/hacker
hacker@dojo:~$
```
Now it's your turn. I've hidden the flag in a random directory on the filesystem. It's still called flag. Go find it!

Several notes. First, there are other files named flag on the filesystem. Don't panic if the first one you try doesn't have the actual flag in it. Second, there're plenty of places in the filesystem that are not accessible to a normal user. These will cause find to generate errors, but you can ignore those; we won't hide the flag there! Finally, find can take a while; be patient!

### Solve
**Flag:** `pwn.college{Ym2n1lWKCWY5AKTtHydHjN1ZzxD.QXyMDO0wCM4kjNzEzW}`

I first navigated to / in order to see what files were in the root. Then I searched each directory in / for anything that matched flag. /usr had two paths that matched. Then I explored each of those paths till I found the flag itself.

```
hacker@commands~finding-files:~$ cd /
hacker@commands~finding-files:/$ ls
bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~finding-files:/$ find /lib -name flag
hacker@commands~finding-files:/$ find /lib32 -name flag
hacker@commands~finding-files:/$ find /lib64 -name flag
hacker@commands~finding-files:/$ find /libx32 -name flag
hacker@commands~finding-files:/$ find /usr -name flag
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/usr/share/javascript/mathjax/jax/output/SVG/fonts/Neo-Euler/Marks/Regular/flag
hacker@commands~finding-files:/$ ls /usr/local/lib/python3.8/dist-packages/pwnlib/flag
__init__.py  __pycache__  flag.py
hacker@commands~finding-files:/$ ls /usr/share/javascript/mathjax/jax/output/SVG/fonts/Neo-Euler/Marks/Regular/flag
/usr/share/javascript/mathjax/jax/output/SVG/fonts/Neo-Euler/Marks/Regular/flag
hacker@commands~finding-files:/$ cat /usr/share/javascript/mathjax/jax/output/SVG/fonts/Neo-Euler/Marks/Regular/flag
pwn.college{Ym2n1lWKCWY5AKTtHydHjN1ZzxD.QXyMDO0wCM4kjNzEzW}hacker@commands~finding-files:/$
```

### New Learnings
I learned how to use find effectively to search large parts of the filesystem for a specific filename. I practiced scoping searches to likely directories (e.g. /usr, /lib, /home), ignoring permission errors, and then verifying candidates with ls and cat. I also learned to be patient with find on / and to explore multiple matches because many files can share the same name.



## Symbolic Links
