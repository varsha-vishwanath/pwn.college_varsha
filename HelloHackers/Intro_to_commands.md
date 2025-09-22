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
