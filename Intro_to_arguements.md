# Hello Hackers

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
I learnt what an arguement was, the difference between an arguement and a command and the structure of a shell command.
