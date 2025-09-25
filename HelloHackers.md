# Hello Hackers

## Intro to Commands
  In this challenge, you will invoke your first command! When you type a command and hit enter, the command will be invoked, as so:
  ```
  hacker@dojo:~$ whoami
  hacker
  hacker@dojo:~$
  ```
  
  Here, the user executed the whoami command, which simply prints the username (hacker) to the terminal. When the command terminates, the shell once again displays the prompt, ready for the next command.

  In this level, invoke the hello command to get the flag! Keep in mind: commands in Linux are case sensitive: hello is different from HELLO.
### Solve

**Flag:** `pwn.college{0QIImS4ZxISkMaewpecLRTxRgf7.QX3YjM1wCM4kjNzEzW}`

```
hacker@hello~intro-to-commands:~$ whoami
hacker
hacker@hello~intro-to-commands:~$ hello
Success! Here is your flag:
pwn.college{0QIImS4ZxISkMaewpecLRTxRgf7.QX3YjM1wCM4kjNzEzW}  
```

Solving this challenge was simple as the instructions were given. I had to type in "hello" as the command that returned the flag.

### New Learnings
Since this was the first challenge, I learnt how to connect to the pwn.college challenge using ssh and how to type in a command in linux.



## Intro to Arguements
Let's try something more complicated: a command with arguments, which is what we call additional data passed to the command. When you type a line of text and hit enter, the shell actually parses your input into a command and its arguments. The first word is the command, and the subsequent words are arguments. Observe:
```
hacker@dojo:~$ echo Hello
Hello
hacker@dojo:~$
```
In this case, the command was echo, and the argument was Hello. echo is a simple command that "echoes" all of its arguments back out onto the terminal, like you see in the session above.

Let's look at echo with multiple arguments:
```
hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
hacker@dojo:~$
```
In this case, the command was echo, and Hello and Hackers! were the two arguments to echo. Simple!

In this challenge, to get the flag, you must run the hello command (NOT the echo command) with a single argument of hackers. Try it now!

### Solve
**Flag:** `pwn.college{0QIImS4ZxISkMaewpecLRTxRgf7.QX3YjM1wCM4kjNzEzW}`
```
hacker@hello~intro-to-commands:~$ hello hackers
Success! Here is your flag:
pwn.college{0QIImS4ZxISkMaewpecLRTxRgf7.QX3YjM1wCM4kjNzEzW}
```

### New Learnings
I learnt what an arguement was, the difference between an arguement and a command, and the structure of a shell command.



## Command History
You're going to type a lot of commands, and typing everything from scratch can be annoying. Luckily, the shell saves a history of every command you invoke.

You can scroll through those saved commands with the up/down arrow keys, and we'll practice that in this challenge. This challenge will inject the flag into your history. Bring up a terminal, hit the up arrow, and grab it! In other challenges, the history will contain the log of the commands you've run, so if you need to run a similar command again, you can use the arrow keys to scroll through and find it!

### Solve
**Flag:** `pwn.college{wdBgtxlR83LLy9nbFZX6_Awb2Va.0lNzEzNxwCM4kjNzEzW}`

```
hacker@hello~intro-to-commands:~$ the flag is pwn.college{wdBgtxlR83LLy9nbFZX6_Awb2Va.0lNzEzNxwCM4kjNzEzW}
```

### New Learnings
I learnt that the shell saves previously executed commands and that i can use/ view those commands again by toggling the up and down arrows to retrieve them.
