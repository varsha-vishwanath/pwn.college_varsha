# Shell Variables

## Printing Variables
Let's start with printing variables out. The /challenge/run program will not, and cannot, give you the flag, but that's okay, because the flag has been put into the variable called "FLAG"! Just have your shell print it out!

You can accomplish this using a number of ways, but we'll start with echo. This command just prints stuff. For example:
```
hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
```
You can also print out variables with echo, by prepending the variable name with a $. For example, there is a variable, PWD, that always holds the current working directory of the current shell. You print it out as so:
```
hacker@dojo:~$ echo $PWD
/home/hacker
```
Now it's your turn. Have your shell print out the FLAG variable and solve this challenge!

### Solve
**Flag:** `pwn.college{0u8kVr9jRTzxRNyae_yVoHNV0q0.QX3UTN0wCM4kjNzEzW}`

```
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{0u8kVr9jRTzxRNyae_yVoHNV0q0.QX3UTN0wCM4kjNzEzW}
```

### New Learnings
I learned how to read shell variables by prefixing the variable name with $. Using echo $FLAG printed the contents of the FLAG variable to the terminal.



## Setting Variables
Naturally, as well as reading values stored in variables, you can write values to variables. This is done, as with many other languages, using =. To set variable VAR to value 1337, you would use:
```
hacker@dojo:~$ VAR=1337
```
Note that there are no spaces around the =! If you put spaces (e.g., VAR = 1337), the shell won't recognize a variable assignment and will, instead, try to run the VAR command (which does not exist).

Also note that this uses VAR and not $VAR: the $ is only prepended to access variables. In shell terms, this prepending of $ triggers what is called variable expansion, and is, surprisingly, the source of many potential vulnerabilities (if you're interested in that, check out the Art of the Shell dojo when you get comfortable with the command line!).

After setting variables, you can access them using the techniques you've learned previously, such as:
```
hacker@dojo:~$ echo $VAR
1337
```
To solve this level, you must set the PWN variable to the value COLLEGE. Be careful: both the names and values of variables are case-sensitive! PWN is not the same as pwn and COLLEGE is not the same as College.

### Solve
**Flag:** `pwn.college{oLJMpiRWFW6ix1I3YJ_gmZfg3tQ.QX5UTN0wCM4kjNzEzW}`

```
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{oLJMpiRWFW6ix1I3YJ_gmZfg3tQ.QX5UTN0wCM4kjNzEzW}
```

### New Learnings
I learned how to set shell variables: use NAME=value with no spaces around the = and then read it with echo $NAME. I also learned that variable names and values are case‑sensitive, so PWN is different from pwn, and COLLEGE is different from College.



## Multi-Word Variables
In this level, you will learn about quoting. Spaces have special significance in the shell, and there are places where you can't use them spuriously. Recall our variable setting:
```
hacker@dojo:~$ VAR=1337
```
That sets the VAR variable to 1337, but what if you wanted to set it to 1337 SAUCE? You might try the following:
```
hacker@dojo:~$ VAR=1337 SAUCE
```
This looks reasonable, but it does not work, for similar reasons to needing to have no spaces around the =. When the shell sees a space, it ends the variable assignment and interprets the next word (SAUCE in this case) as a command. To set VAR to 1337 SAUCE, you need to quote it:
```
hacker@dojo:~$ VAR="1337 SAUCE"
```
Here, the shell reads 1337 SAUCE as a single token, and happily sets that value to VAR. In this level, you'll need to set the variable PWN to COLLEGE YEAH. Good luck!

### Solve
**Flag:** `pwn.college{ktIpFucIQwoaRKo9MhlID9oq2b8.QXwYTN0wCM4kjNzEzW}`

```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{ktIpFucIQwoaRKo9MhlID9oq2b8.QXwYTN0wCM4kjNzEzW}
```

### New Learnings
I learned why quoting matters in the shell. Spaces separate tokens, so to assign a multi‑word value you must quote it. Here, PWN="COLLEGE YEAH" stores the entire string as one variable.



## Exporting Variables
By default, variables that you set in a shell session are local to that shell process. That is, other commands you run won't inherit them. You can experiment with this by simply invoking another shell process in your own shell, like so:
```
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ echo "VAR is: $VAR"
VAR is: 1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is:
``` 
In the output above, the $ prompt is the prompt of sh, a minimal shell implementation that is invoked as a child of the main shell process. And it does not receive the VAR variable!

This makes sense, of course. Your shell variables might have sensitive or weird data, and you don't want it leaking to other programs you run unless it explicitly should. How do you mark that it should? You export your variables. When you export your variables, they are passed into the environment variables of child processes. You'll encounter the concept of environment variables in other challenges, but you'll observe their effects here. Here is an example:
```
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ export VAR
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```
Here, the child shell received the value of VAR and was able to print it out! You can also combine those first two lines.
```
hacker@dojo:~$ export VAR=1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```
In this challenge, you must invoke /challenge/run with the PWN variable exported and set to the value COLLEGE, and the COLLEGE variable set to the value PWN but not exported (e.g., not inherited by /challenge/run). Good luck!

### Solve
**Flag:** `pwn.college{g5yK1hj0173jmE9KnIV2AbB_paF.QXyYTN0wCM4kjNzEzW}`

```
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ export PWN=COLLEGE
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ sh
sh-5.2$ /challenge/run
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great
job! Here is your flag:
pwn.college{g5yK1hj0173jmE9KnIV2AbB_paF.QXyYTN0wCM4kjNzEzW}
```

### New Learnings
I learned the difference between shell variables and environment (exported) variables. export PWN=COLLEGE passed PWN into the environment so /challenge/run could see it, while COLLEGE=PWN without export remained local to my shell and was not inherited.



## Printing Exported Variables
There are multiple ways to access variables in bash. echo was just one of them, and we'll now learn at least one more in this challenge.

Try the env command: it'll print out every exported variable set in your shell, and you can look through that output to find the FLAG variable!

### Solve
**Flag:** `pwn.college{MbfrcX4x4o6Z7RukBRTCHautA2E.QX4UTN0wCM4kjNzEzW}`

```
hacker@variables~printing-exported-variables:~$ env
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
PWD=/home/hacker
MANPATH=/run/dojo/share/man:
DOJO_AUTH_TOKEN=f20e10185612007b229833353d9da07aa6be8b980f14e5f34f4db1b97cafdb26
HOME=/home/hacker
LANG=C.UTF-8
FLAG=pwn.college{MbfrcX4x4o6Z7RukBRTCHautA2E.QX4UTN0wCM4kjNzEzW}
TERMINFO=/run/dojo/share/terminfo
TERM=xterm-256color
SHLVL=2
LC_CTYPE=C.UTF-8
SSL_CERT_FILE=/run/dojo/etc/ssl/certs/ca-bundle.crt
PATH=/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
DEBIAN_FRONTEND=noninteractive
_=/run/dojo/bin/env
```

### New Learnings
I learned that env lists every exported environment variable in the current shell (unlike echo $VAR, which prints a single variable).



## Storing Command Output
In the course of working with the shell, you will often want to store the output of some command into a variable. Luckily, the shell makes this quite easy using something called Command Substitution! Observe:
```
hacker@dojo:~$ FLAG=$(cat /flag)
hacker@dojo:~$ echo "$FLAG"
pwn.college{blahblahblah}
hacker@dojo:~$
```
Neat! Now, you practice. Read the output of the /challenge/run command directly into a variable called PWN, and it will contain the flag!

Trivia: You can also use backticks instead of $(): FLAG=`cat /flag` instead of FLAG=$(cat /flag) in the example above. This is an older format, and has some disadvantages (for example, imagine if you wanted to nest command substitutions. How would you do $(cat $(find / -name flag)) with backticks? The official stance of pwn.college is that you should use $(blah) instead of `blah`.

### Solve
**Flag:** `pwn.college{cLMkrDJyBedmWulVzPRtAg_anry.QX1cDN1wCM4kjNzEzW}`

```
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
Congratulations! You have read the flag into the PWN variable. Now print it out
and submit it!
hacker@variables~storing-command-output:~$ echo "$PWN"
pwn.college{cLMkrDJyBedmWulVzPRtAg_anry.QX1cDN1wCM4kjNzEzW}
```

### New Learnings
I learned that using $(...) runs a command and stores its stdout as the value of a variable. I used PWN=$(/challenge/run) to read the flag into PWN, then echo "$PWN" to print it



## Reading Input
We'll start with reading input from the user (you). That's done using the aptly named read builtin, which reads input into a variable!

Here is an example using the -p argument, which lets you specify a prompt (otherwise, it would be hard for you, reading this now, to separate input from output in the example below):
```
hacker@dojo:~$ read -p "INPUT: " MY_VARIABLE
INPUT: Hello!
hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
You entered: Hello!
```
Keep in mind, read reads data from your standard input! The first Hello!, above, was inputted rather than outputted. Let's try to be more explicit with that. Here, we annotated the beginning of each line with whether the line represents INPUT from the user or OUTPUT to the user:
```
 INPUT: hacker@dojo:~$ echo $MY_VARIABLE
OUTPUT:
 INPUT: hacker@dojo:~$ read MY_VARIABLE
 INPUT: Hello!
 INPUT: hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
OUTPUT: You entered: Hello!
```
In this challenge, your job is to use read to set the PWN variable to the value COLLEGE. Good luck!

### Solve
**Flag:** `pwn.college{oxZQpfJxjIxpDZMPh1ZtJ_Vlxs-.QX4cTN0wCM4kjNzEzW}`

```
hacker@variables~reading-input:~$ read PWN
COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{oxZQpfJxjIxpDZMPh1ZtJ_Vlxs-.QX4cTN0wCM4kjNzEzW}
```
I didn't use the -p arguement here, although I understood it, as it wasn't needed.

### New Learnings
I learned how to use read to get input from the user and store it in a variable. By running read PWN and typing COLLEGE, the variable PWN now held that value.



## Reading Files
Often, when shell users want to read a file into an environment variable, they do something like:
```
hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ VAR=$(cat some_file)
hacker@dojo:~$ echo $VAR
test
```
This works, but it represents what grouchy hackers call a "Useless Use of Cat". That is, running a whole other program just to read the file is a waste. It turns out that you can just use the powers of the shell!

Previously, you read user input into a variable. You've also previously redirected files into command input! Put them together, and you can read files with the shell.
```
hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ read VAR < some_file
hacker@dojo:~$ echo $VAR
test
```
What happened there? The example redirects some_file into the standard input of read, and so when read reads into VAR, it reads from the file! Now, use that to read /challenge/read_me into the PWN environment variable, and we'll give you the flag! The /challenge/read_me will keep changing, so you'll need to read it right into the PWN variable with one command!

### Solve
**Flag:** `pwn.college{IzfYtRYYUln_qrqvydW3Uh_-R-S.QXwIDO0wCM4kjNzEzW}`

```
hacker@variables~reading-files:~$ read PWN < <(/challenge/read_me)
You appear to be invoking a subshell. This could be, for example, because you
are doing something like `PWN=$(echo COLLEGE)`. Instead, you must use `read` to
set the PWN variable.
hacker@variables~reading-files:~$ read PWN < /challenge/read_me
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{IzfYtRYYUln_qrqvydW3Uh_-R-S.QXwIDO0wCM4kjNzEzW}
```
I misunderstood and incorrectly assumed that /challenge/read_me was a command so I was not able to get the flag as I was invoking a subshell. 

### New Learnings
I learned how to load a file into a shell variable without spawning extra processes: read PWN < /challenge/read_me reads the file directly into PWN.
