# File Globbing

## Matching with *
The first glob we'll learn is *. When it encounters a * character in any argument, the shell will treat it as a "wildcard" and try to replace that argument with any files that match the pattern. It's easier to show you than explain:
```
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_*
Look: file_a file_b file_c
```
Of course, though in this case, the glob resulted in multiple arguments, it can just as simply match only one. For example:
```
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: file_*
Look: file_a
```
When zero files are matched, by default, the shell leaves the glob unchanged:
```
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: nope_*
Look: nope_*
```
The * matches any part of the filename except for / or a leading . character. For example:
```
hacker@dojo:~$ echo ONE: /ho*/*ck*
ONE: /home/hacker
hacker@dojo:~$ echo TWO: /*/hacker
TWO: /home/hacker
hacker@dojo:~$ echo THREE: ../*
THREE: ../hacker
```
Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use globbing to keep the argument you pass to cd to at most four characters! Once you're there, run /challenge/run for the flag!

### Solve
**Flag:** `pwn.college{AwDCQdNI_XQqT0D-_roB17YNi5h.QXxIDO0wCM4kjNzEzW}`

```
hacker@globbing~matching-with-:/challenge$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{AwDCQdNI_XQqT0D-_roB17YNi5h.QXxIDO0wCM4kjNzEzW}
```

### New Learnings
I learnt how globbing works. The * wildcard in an argument is expanded by the shell to match filenames (but not / or leading .). Using cd /ch* matched /challenge, so I could change into the directory while keeping the typed argument short.



## Matching with ?
Next, let's learn about ?. When it encounters a ? character in any argument, the shell will treat it as a single-character wildcard. This works like *, but only matches one character. For example:
```
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_cc
hacker@dojo:~$ ls
file_a	file_b	file_cc
hacker@dojo:~$ echo Look: file_?
Look: file_a file_b
hacker@dojo:~$ echo Look: file_??
Look: file_cc
```
Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use the ? character instead of c and l in the argument to cd! Once you're there, run /challenge/run for the flag!

### Solve
**Flag:** `pwn.college{AfvRMujjTTKhEVlVdww0Bpjc2tp.QXyIDO0wCM4kjNzEzW}`

```
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{AfvRMujjTTKhEVlVdww0Bpjc2tp.QXyIDO0wCM4kjNzEzW}
```

### New Learnings
I learnt about the ? glob: it matches exactly one character (not / and not a leading .). By using cd /?ha??enge the shell expanded the pattern to /challenge.



## Matching with []
Next, we will cover []. The square brackets are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets. For example, [pwn] will match the character p, w, or n. For example:
```
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```
Try it here! We've placed a bunch of files in /challenge/files. Change your working directory to /challenge/files and run /challenge/run with a single argument that bracket-globs into file_b, file_a, file_s, and file_h!

### Solve
**Flag:** `pwn.college{YowQmFHHlYsF8dRu6jN3vGJbttX.QXzIDO0wCM4kjNzEzW}`

```
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{YowQmFHHlYsF8dRu6jN3vGJbttX.QXzIDO0wCM4kjNzEzW}
```

### New Learnings
I learnt how to use square brackets [] for globbing: they let you match a specific set of characters in a filename instead of any character like ? or *. Using file_[bash] matched multiple specific files at once (file_b, file_a, file_s, file_h).



## Matching Paths with []
Globbing happens on a path basis, so you can expand entire paths with your globbed arguments. For example:
```
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: /home/hacker/file_[ab]
Look: /home/hacker/file_a /home/hacker/file_b
```
Now it's your turn. Once more, we've placed a bunch of files in /challenge/files. Starting from your home directory, run /challenge/run with a single argument that bracket-globs into the absolute paths to the file_b, file_a, file_s, and file_h files!

### Solve
**Flag:** `pwn.college{ApqZb1gUMvQoCWs8BII3NRfKauL.QX0IDO0wCM4kjNzEzW}`

```
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{ApqZb1gUMvQoCWs8BII3NRfKauL.QX0IDO0wCM4kjNzEzW}
```

### New Learnings
I learnt that shell globbing applies to entire paths, not just the final filename. By using /challenge/files/file_[bash] the shell expanded the pattern into the absolute paths /challenge/files/file_b, /challenge/files/file_a, /challenge/files/file_s, and /challenge/files/file_h, letting me pass all four files to the program in one go.


## Multiple Globs
So far, you've specified one glob at a time, but you can do more! Bash supports the expansion of multiple globs in a single word. For example:
```
hacker@dojo:~$ cat /*fl*
pwn.college{YEAH}
hacker@dojo:~$
```
What happens above is that the shell looks for all files in / that start with anything (including nothing), then have an f and an l, and end in anything (including ag, which makes flag).

Now you try it. We put a few happy, but diversely-named files in /challenge/files. Go cd there and run /challenge/run, providing a single argument: a short (3 characters or less) globbed word with two * globs in it that covers every word that contains the letter p.

### Solve
**Flag:** `pwn.college{Q6_YEoyjvJl3pSP_x8NqUwmsJpz.0lM3kjNxwCM4kjNzEzW}`

```
hacker@globbing~multiple-globs:~$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{Q6_YEoyjvJl3pSP_x8NqUwmsJpz.0lM3kjNxwCM4kjNzEzW}
```

### New Learnings
I learned that globs can be combined inside a single word — the shell expands each glob before running the command. By using *p* I matched every filename containing the letter p.



## Mixing Globs
Now, let's put the previous levels together! We put a few happy, but diversely-named files in /challenge/files. Go cd there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to /challenge/run) will match the files "challenging", "educational", and "pwning"!

### Solve
**Flag:** `pwn.college{wSBpOHEZ3ZbumzjyW0yqK2bbiA3.QX1IDO0wCM4kjNzEzW}`

The challenge seemed straightforward although I forgot that there were multiple other files in the specified directory and that my globbing would have to isolate "challenging", "pwning" and "educational". That was tricky until I looked at the files and realized each word started with a different letter of the alphabet. Then it became a matter of globbing such that I isolated the words that started with c, e and p.

```
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run *i*n*
Error: you did not use a square bracket glob...
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run *i*[gl]
Error: your argument is too long! It must be 6 characters or less.
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run *[gl]
Your expansion did not expand to the requested files (challenging, educational,
pwning). Instead, it expanded to:
amazing beautiful challenging delightful educational jovial laughing magical pwning thrilling uplifting wonderful xenial youthful
hacker@globbing~mixing-globs:/challenge/files$ ls
amazing      delightful   great       jovial    magical     pwning   splendid   victorious  youthful
beautiful    educational  happy       kind      nice        queenly  thrilling  wonderful   zesty
challenging  fantastic    incredible  laughing  optimistic  radiant  uplifting  xenial
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{wSBpOHEZ3ZbumzjyW0yqK2bbiA3.QX1IDO0wCM4kjNzEzW}
```

### New Learnings
This challenge reinforced how flexible globbing can be when combining patterns. By using [cep]*, I could match multiple filenames that start with specific letters (c, e, or p) in a single, short argument.



## Exclusionary Globbing
Sometimes, you want to filter out files in a glob! Luckily, [] helps you do just this. If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and that bracket instance matches characters that aren't listed. For example:
```
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[!ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[^ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```
Armed with this knowledge, go forth to /challenge/files and run /challenge/run with all files that don't start with p, w, or n!

NOTE: The ! character has a different special meaning in bash when it's not the first character of a [] glob, so keep that in mind if things stop making sense! ^ does not have this problem, but is also not compatible with older shells.

### Solve
**Flag:** `pwn.college{YzXJqBgKtZIlUboD7IKQCEzoLW6.QX2IDO0wCM4kjNzEzW}`

```
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [^pwn]*
You got it! Here is your flag!
pwn.college{YzXJqBgKtZIlUboD7IKQCEzoLW6.QX2IDO0wCM4kjNzEzW}
```

### New Learnings
I learnt exclusionary globbing. Placing ! or ^ as the first character inside [] inverts the set. In this case, [^pwn]* expands to every filename not starting with p, w, or n.



## Tab Completion
As tempting as it might be, using * to shorten what must be typed on the commandline can lead to mistakes. Your glob might expand to unintended files, and you might not spot it until the rm command is already running! No one is safe from this style of error.

A safer alternative when you are trying to specify a specific target is tab completion. If you hit tab in the shell, it'll try to figure out what you're going to type and automatically complete it. Auto-completion is super useful, and this challenge will explore its use in specifying files.

This challenge has copied the flag into /challenge/pwncollege, and you can freely cat that file. But you can't type the filename: we used some serious trickery to make sure that you must tab-complete it. Try it out!
```
hacker@dojo:~$ ls /challenge
DESCRIPTION.md  pwncollege
hacker@dojo:~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@dojo:~$ cat /challenge/pwn<TAB>
pwn.college{HECK YEAH}
hacker@dojo:~$
```
When you hit that tab key, the name will expand and you'll be able to read the file. Good luck!

### Solve
**Flag:** `pwn.college{sWGhQ7TySsINR3Y-8oxf6fn2uCG.0FN0EzNxwCM4kjNzEzW}`

```
hacker@globbing~tab-completion:~$ cd /challenge/pwncollege
bash: cd: /challenge/pwncollege: No such file or directory
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege​
pwn.college{sWGhQ7TySsINR3Y-8oxf6fn2uCG.0FN0EzNxwCM4kjNzEzW}
```

### New Learnings
I learned tab completion: pressing Tab lets the shell expand partially typed names into the correct filename, avoiding typing mistakes and risky globs.



## Multiple Options for Tab Completion
Consider the following situation:
```
hacker@dojo:~$ ls
flag  flamingo  flowers
hacker@dojo:~$ cat f<TAB>
```
There are multiple options! What happens?

What happens varies based on the specific shell and its options. By default bash will auto-expand until the first point when there are multiple options (in this case, fl). When you hit tab a second time, it'll print out those options. Other shells and configurations, instead, will cycle through the options.

This challenge has a /challenge/files directory with a bunch of files starting with pwncollege. Tab-complete from /challenge/files/p or so, and make your way to the flag!

### Solve
**Flag:** `pwn.college{40lAxy0r1ROfS4CyCaq7icYlzdE.0lN0EzNxwCM4kjNzEzW}`

```
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwn
pwn                    pwn-the-planet         pwncollege-flag        pwncollege-flyswatter
pwn-college            pwncollege-family      pwncollege-flamingo    pwncollege-hacking
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-flag
pwn.college{40lAxy0r1ROfS4CyCaq7icYlzdE.0lN0EzNxwCM4kjNzEzW}
```

### New Learnings
I learned how tab completion behaves when there are multiple matches: the shell completes up to the longest common prefix (e.g. pwn) and shows all matching candidates on a second Tab. Using this, I navigated /challenge/files interactively and selected pwncollege-flag to read the flag.



## Tab Completion on Commands
Tab completion is for more than files! You can also tab-complete commands. This level has a command that starts with pwncollege, and it'll give you the flag. Type pwncollege and hit the tab key to auto-complete it!

NOTE: You can auto-complete any command, but be careful: callous auto-completes without double-checking the result can wreak havoc in your shell if you accidentally run the wrong commands!

### Solve
**Flag:** `pwn.college{YrXwGPKds-I5scEGRDSosqmclVf.0VN0EzNxwCM4kjNzEzW}`

```
hacker@globbing~tab-completion-on-commands:~$ pwncollege-30622
Correct! Here is your flag:
pwn.college{YrXwGPKds-I5scEGRDSosqmclVf.0VN0EzNxwCM4kjNzEzW}
```

### New Learnings
I learned that tab completion works for commands, not just files. Auto-completing pwncollege… saved typing and let me run the exact program quickly.
