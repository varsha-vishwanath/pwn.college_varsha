# Data Manipulation

## Translating Characters
One of the purposes of piping data is to modify it. Many Linux commands will help you modify data in really cool ways. One of these is tr, which translates characters it receives over standard input and prints them to standard output.

In its most basic usage, tr translates the character provided in its first argument to the character provided in its second argument:
```
hacker@dojo:~$ echo OWN | tr O P
PWN
hacker@dojo:~$
```
It can also handle multiple characters, with the characters in different positions of the first argument replaced with associated characters in the second argument.
```
hacker@dojo:~$ echo PWM.COLLAGE | tr MA NE
PWN.COLLEGE
hacker@dojo:~$
```
Now, you try it! In this level, /challenge/run will print the flag but will swap the casing of all characters (e.g., A will become a and vice-versa). Can you undo it with tr and get the flag?

### Solve
**Flag:** `pwn.college{4pDPkLA02SJ9bHwy0m2PclFS33d.01MxEzNxwCM4kjNzEzW}`

I initially messed up as I assumed that I had to make the case of the flag uniform (i assumed the entire flag would be either uppercase or lowercase) and ignored that the flag had a mix of uppercase and lwoercase letters. Therefore the flag that was returned didn't work. But when I realized this issue, I was able to look up how to correctly map the letters and got the correct flag.

```
hacker@data~translating-characters:~$ /challenge/run | tr 'a-zA-Z' 'A-Za-z'
yOUR CASE-SWAPPED FLAG:
pwn.college{4pDPkLA02SJ9bHwy0m2PclFS33d.01MxEzNxwCM4kjNzEzW}
```

### New Learnings
I learned that tr can map entire character ranges, not just single characters. By providing a-zA-Z as the input set and A-Za-z as the output set, each lowercase letter becomes uppercase and vice-versa.

### References
https://stackoverflow.com/questions/23178769/unix-tr-command-to-convert-lower-case-to-upper-and-upper-to-lower-case



## Deleting Characters
tr can also translate characters to nothing (i.e., delete them). This is done via a -d flag and an argument of what characters to delete:
```
hacker@dojo:~$ echo PAWN | tr -d A
PWN
hacker@dojo:~$
```
Pretty simple! Now you give it a try. I'll intersperse some decoy characters (specifically: ^ and %) among the flag characters. Use tr -d to remove them!

### Solve
**Flag:** `pwn.college{EycLcZZ-kdm9y7n5CY65vJTPHBK.0FNxEzNxwCM4kjNzEzW}`

```
hacker@data~deleting-characters:~$ /challenge/run | tr -d ^%
Your character-stuffed flag:
pwn.college{EycLcZZ-kdm9y7n5CY65vJTPHBK.0FNxEzNxwCM4kjNzEzW}
```

### New Learnings
I learned how to remove unwanted characters from a stream using tr -d. By piping the noisy output into tr -d ^% I removed out the ^ and % characters and recovered the clean flag.



## Deleting Newlines
A common class of characters to remove is a line separator. This happens when you have a stream of data that you want to turn into a single line for further processing. You can specify newlines almost like any other character, by escaping them:
```
hacker@dojo:~$ echo "hello_world!" | tr _ "\n"
hello
world!
hacker@dojo:~$
```
Here, the backslash (\) signifies that the character that follows it is a standin for a character that's hard to input into the shell normally. The newline, of course, is hard to input because when you typically hit Enter, you'll run the command itself. \n is a standin for this newline, and it must be in quotes to prevent the shell interpreter itself from trying to interpret it and pass it to tr instead.

Now, let's combine this with deletion. In this challenge, we'll inject a bunch of newlines into the flag. Delete them with tr's -d flag and the escaped newline specification!

Fun fact! Want to actually replace a backslash (\) character? Because \ is the escape character, you gotta escape it! \\ will be treated as a backslash by tr. This isn't relevant to this challenge, but is a fun fact nonetheless!

### Solve
**Flag:** `pwn.college{0wNMr8kZ_yr8zfZi_FU_9OZXe_I.0VNxEzNxwCM4kjNzEzW}`

```
hacker@data~deleting-newlines:~$ /challenge/run | tr -d '\n'
Your line-split flag: pwn.college{0wNMr8kZ_yr8zfZi_FU_9OZXe_I.0VNxEzNxwCM4kjNzEzW}hacker@data~deleting-newlines:~$
```

### New Learnings
I learned how to remove newline characters with tr -d '\n' so that multi-line output becomes a single continuous line. I also learned about special characters in the shell.



## Extracting the First Lines with Head
In your Linux journey, you'll experience situations where you need to grab just the early output of very verbose programs. For this, you'll reach for head! The head command is used to display the first few lines of its input:
```
hacker@dojo:~$ cat /something/very/long | head
this
is
just
the
first
ten
lines
of
the
file
hacker@dojo:~$
```
By default, it shows the first 10 lines, but you can control this with the -n option:
```
hacker@dojo:~$ cat /something/very/long | head -n 2
this
is
hacker@dojo:~$
```
This challenge's /challenge/pwn outputs a bunch of data, and you'll need to pipe it through head to grab just the first 7 lines and then pipe them onwards to /challenge/college, which will give you the flag if you do this right! Your solution will be a long composite command with two pipes connecting three commands. Good luck!

### Solve
**Flag:** `pwn.college{ImbCJ0AdkBOLrNDbQWk-WxC7va8.0lNxEzNxwCM4kjNzEzW}`

```
hacker@data~extracting-the-first-lines-with-head:~$ /challenge/pwn | head -n 7 | /challenge/college
Congratulations, you piped the right codes!
pwn.college{ImbCJ0AdkBOLrNDbQWk-WxC7va8.0lNxEzNxwCM4kjNzEzW}
```

### New Learnings
I learned how to trim output using head. By piping /challenge/pwn into head -n 7 I extracted only the first seven lines and then piped that output into /challenge/college to get the flag.



## Extracting Specific Sections of Text
Sometimes, you want to grab specific columns of data, such as the first column, the third column, or the 42nd column. For this, there's the cut command.

For example, imagine that you have the following data file:
```
hacker@dojo:~$ cat scores.txt
hacker 78 99 67
root 92 43 89
hacker@dojo:~$
```
You could use cut to extract specific columns:
```
hacker@dojo:~$ cut -d " " -f 1 scores.txt
hacker
root
hacker@dojo:~$ cut -d " " -f 2 scores.txt
78
92
hacker@dojo:~$ cut -d " " -f 3 scores.txt
99
43
hacker@dojo:~$
```
The -d argument specifies the column delimiter (how columns are separated). In this case, it's a space character. Of course, it has to be in quotes here so that the shell knows that the space is an argument rather than a space separating other arguments! The -f argument specifies the field number (which column to extract).

In this challenge, the /challenge/run program will give you a bunch of lines with random numbers and single characters (characters of the flag) as columns. Use cut to extract the flag characters, then pipe them to tr -d "\n" (like the previous level!) to join them together into a single line. Your solution will look something like /challenge/run | cut ??? | tr ???, with the ??? filled out.

### Solve
**Flag:** `pwn.college{AaEr2g4sO8Oe-qsgZiHh_TYINbz.01NxEzNxwCM4kjNzEzW}`

```
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run
27456 p
18953 w
21968 n
28844 .
13937 c
25315 o
19718 l
26897 l
24716 e
12479 g
28762 e
20634 {
16342 A
13360 a
17814 E
12371 r
9227 2
21105 g
31833 4
15255 s
30122 O
184 8
14463 O
11627 e
3058 -
17717 q
6927 s
30256 g
29891 Z
14853 i
22166 H
9086 h
10869 _
10419 T
5044 Y
8213 I
18340 N
31473 b
31256 z
19345 .
13560 0
9610 1
18521 N
27132 x
10571 E
31608 z
10822 N
2581 x
7672 w
5307 C
14387 M
16136 4
24103 k
29810 j
31408 N
27746 z
10073 E
795 z
1526 W
2122 }
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run | cut -d " " -f 2
p
w
n
.
c
o
l
l
e
g
e
{
A
a
E
r
2
g
4
s
O
8
O
e
-
q
s
g
Z
i
H
h
_
T
Y
I
N
b
z
.
0
1
N
x
E
z
N
x
w
C
M
4
k
j
N
z
E
z
W
}
hacker@data~extracting-specific-sections-of-text:~$  /challenge/run | cut -d " " -f 2 | tr -d "\n"
pwn.college{AaEr2g4sO8Oe-qsgZiHh_TYINbz.01NxEzNxwCM4kjNzEzW}hacker@data~extracting-specific-sections-of-text:~$
```

### New Learnings
I learned how to use cut to extract specific columns from whitespace-separated data (cut -d " " sets the delimiter and -f 2 picks the second column). Piping that into tr -d '\n' collapsed the per-line characters into a single line.



## Sorting Data
Files (or output lines of commands) aren't always in the order you need them! The sort command helps you organize data. It reads lines from input (or files) and outputs them in sorted order:
```
hacker@dojo:~$ cat names.txt
  hack
  the
  planet
  with
  pwn
  college
hacker@dojo:~$ sort names.txt
  college
  hack
  planet
  pwn
  the
  with
hacker@dojo:~$
```
By default, sort orders lines alphabetically. Arguments can change this:

* -r: reverse order (Z to A)
* -n: numeric sort (for numbers)
* -u: unique lines only (remove duplicates)
* -R: random order!
  
In this challenge, there's a file at /challenge/flags.txt containing 100 fake flags, with the real flag mixed among them. When sorted alphabetically, the real flag will be at the end (we made sure of this when generating fake flags). Go get it!

### Solve 
**Flag:** `pwn.college{ggh8VMaLFGfwt8-eREMR1jL14d9.0FM0MDOxwCM4kjNzEzW}`

```
hacker@data~sorting-data:~$ sort -r /challenge/flags.txt
pwn.college{ggh8VMaLFGfwt8-eREMR1jL14d9.0FM0MDOxwCM4kjNzEzW}
pwn.college{ggh8VMaLFGfwt8-eREMR1jL14d9.0FM0MDOxwCM4kjNzEzW}
pwn.college{ggh8VMaLFGfwt8-eREMR1jL14d9.0FM0MDOxwCM4kjNzEyW}
pwn.college{ggh8VMaLFGfwt8-eREMR1jL14d9.0FM0MDOxwCM4kjNzDzW}
pwn.college{ggh8VMaLFGfwt8-eREMR1jL14d9.0FM0MDOxwBM3kjNzEyV}
pwn.college{ggh8VMaLFGfwt8-eREMQ0jL14d9.0FM0MDOxwCM4kjNzEzW}
pwn.college{ggh8VMaLFGfwt8-eRDMR1jL14d8.0FM0MDOxwCL4kjNzEzW}
pwn.college{ggh8VMaLFGfwt8-dREMR1jL14d9.0FM0MDOxwCL4kjNzEzW}
pwn.college{ggh8VMaLFGfwt7-eREMR1iL14d9.0FM0MDNxwCM4kiNzEzW}
pwn.college{ggh8VLaKFGfwt8-eREMR1jL14d9.0FM0MDOxwCM4kjNzEzW}
pwn.college{ggh8UMaLFGfwt8-eREMR1jL14d9.0EM0MDOxwCM4kjNzEzW}
pwn.college{ggg8ULaKFFfwt8-eREMR1jL04c9.0FL0LDOxwCM4kjNyDyW}
pwn.college{gfh8VMaLFGfwt8-eREMR1jL14d9.0FM0MDOxwCM4kjNzEzW}
pwn.college{gfh8VMaLEGfwt8-eREMR1jL14d8.0FM0MDOwvCM4jjNzEzW}
pwn.college{gfh8VMaKFFfws8-eQEMR1jL14d9.0FM0MDOxwCM4kjNzEzV}
pwn.college{gfh7VMaLFGfwt8-eREMR1jL14d9.0FM0MDOxwBM4jiNzEzW}
pwn.collegd{ggh8VMaLFGfwt8-eREMQ0jL04d8.0EM0MDOxwCM4kjMyEzW}
pwn.collegd{ggh8VMaLFGfwt7-eREMR1jL14d9.0FM0MDOxwCM4kjNzEzW}
pwn.collegd{ggh8VLaLFGewt8-eQELQ1iL13d9.0FM0MDOxwCM4kjNzEzW}
pwn.collegd{ggg7VMaKFGfwt8-eRELR0jL04c9.0FM0MDNwwCM4kjNzEzW}
pwn.collegd{fgh7VLaKFFfws8-eREMR0jL04d8.0FM0MDOxvCM4kjNyEzW}
pwn.colldge{ggh8VMaKFGfwt8-eREMR1jL14d9.0FM0LDOxwBM4jjMyEzW}
pwn.colldge{gfg8VLaLFGfws8-eQDMQ1jK03d9.0EL0MCNxwCM4kjMzEzW}
pwn.colldgd{ffg8VMaLEGfvt8-dREMR0iK14d9.0EM0LDNxwBM4kjNzEzV}
pwn.colldfe{ggh7UMaLEGfwt8-eREMQ1iL14d9.0FM0LDNxwCL4kjNzEyV}
pwn.colldfe{ggg7VLaLEFevs7-eREMQ0jL14d8.0FM0MDOwvCL4jjNzDyV}
pwn.colldfe{gfh7VMaLFGfwt8-eREMR1iL13c9.0FM0LCOwwCM4jjNzEyW}
pwn.colldfe{ffg8VLaKFFfvt8-dQEMR1jL14d9.0FM0MCOwvBM4jjNzEzV}
pwn.colkege{ggh8VMaLFFfwt7-eREMR1jL14d8.0FM0MDOxwCM4kjNzEzV}
pwn.colkege{ffg8VMaLFGewt8-eREMQ1jL13d9.0FM0LDOxwCM4kiNzEzW}
pwn.colkegd{ggg8ULaKEFfvs8-eQEMR1iL04d9.0FL0MDNxvBL4kiMyEzV}
pwn.coklegd{gfh8VLaLFGfwt8-eRDLQ1jK03d8.0EL0LDNxwCM4kiNzDyW}
pwn.cnllege{fgh7VMaKFGewt8-eREMR0iL14c9.0FM0MCOxvCL3jjNzDyW}
pwn.cnlldfe{ggg8UMaKEGfwt8-dRDMR0jL13d9.0FM0MDNxwBL4jjMzEzW}
pwn.cnlkege{fgg7UMaLFGfwt8-eREMQ1jL14d9.0EM0LDOwvCM4jjMzDzW}
pwn.cnlkdgd{ggh8VMaLFFevt8-dRELR1jL03d8.0FM0LCOxwCM3kjNyDzW}
pwn.bollege{ggh8VMaLEGfws8-dQEMR1jK14d9.0FM0MDOxwCM4kjMyDzW}
pwn.bollege{gfh7UMaLEGfws8-eQEMR0jL14d8.0FL0MDNwwBM4kjNyEzW}
pwn.bolkege{ggg8VLaLFGfwt8-eRDMR1jL14d9.0FM0LDOxwCM4kjNzEzW}
pwn.bolkefe{ggh8VMaLFGfwt8-eQELR1jL04d9.0FM0MDOxwCM4kjNzEyW}
pwn.bolkdfe{ggh7VLaLFGewt8-dQELQ0jL04c9.0FM0LDNxwBL3jjNzEzW}
pwn.boklege{ggh8VMaLEFevt8-eQEMR1jK13d9.0FL0MCOxwCM4kjNzEzW}
pwn.boklefe{ggg8VMaLFGewt8-eQEMQ0jL14d9.0FM0LDOxwCM4jjNzEzW}
pwn.boklefe{ggg8ULaLFGevt8-dRELR1iL13c9.0EL0MDNxwCM4kjNzEzW}
pwn.bnllefe{fgh8VMaKFFews8-eQEMR1iK14d9.0EM0MDOxvCL3jjNzEzV}
pwm.college{ggh8VMaLFFfwt8-eREMR1jL14d9.0FM0MDOxwCM4kjNzEzW}
pwm.college{ggh8VMaKFGewt8-eREMR1jL14d8.0FM0MCOxwCM4kjNzEzW}
pwm.college{fgg7UMaLEFfwt8-dRDMR1jL14d8.0FM0LDNxwBM4jjNyEzW}
pwm.collegd{fgg8UMaLFGewt7-dREMR1jK04c9.0FM0LDNxvCM3jjMzEzW}
pwm.collefe{ggh8VMaLFGfvs8-eREMQ1jL14d8.0FM0MDOxvCM4kjNyEyV}
pwm.collefe{ggg8VLaLFGfwt8-eRDMR1jK14d9.0FM0MDNxwBM4kjNzEzW}
pwm.colkegd{ggh7VMaLFGfwt8-eRDMR1iL14d9.0FM0MCOxvCM4kjNzEzW}
pwm.colkefe{ffg8ULaKFFewt7-eRELQ1iK14c8.0FM0LDOwwCM3kjNzDzW}
pwm.colkdge{ffh8VMaLFGfws8-eRDMR1iL13c8.0FM0MCOxwCM4kjMyEzV}
pwm.coklege{ggh8ULaLFGfws8-eRDLR0iK13d8.0EM0LDOwvBL3kjNyEzW}
pwm.coklege{ggh7VMaKEGewt8-dRELR1jK04d9.0FM0MDOxwCM4kjMzEyW}
pwm.cnllege{ggg7VMaLFGfwt8-eREMR1jL03d9.0EM0LDOwvBM4kiMzDzW}
pwm.cnllege{fgh8VMaKEGfwt7-dREMR1jK14d9.0FM0LDOxvBL4jiNzEzV}
pwm.cnlldgd{ggh7UMaLFFewt7-eRELR1iL14d9.0FM0MDOxwCM4kjNyEyW}
pwm.cnlkdfe{fgh7VMaKFFewt8-dQELQ1jL04d8.0FL0MCNxvCM4kjNzDzV}
pwm.bollefe{gfh7VMaKFFewt7-eREMR0iL04c9.0EM0MDNxwCM4kjNzEyV}
pwm.bolldfd{ggh8UMaKFGfvs7-eREMR1jL03d9.0FM0MDOxvBM4kiNyEzW}
pwm.bnlldge{ggh8UMaLFFewt8-dRDMQ1jL04c9.0EM0LDOxwCM4jiNyEzW}
pvn.collegd{ggh8VMaLEGfwt7-eREMR0jL04d9.0FM0LDOxwCM4kjNzEzW}
pvn.collegd{ggh7VMaLFGfwt7-eREMR1jL14d9.0FM0LDOxwCM4kiMyDyW}
pvn.collefe{fgh7VMaLFFfvs7-dRELR1jL04c9.0FL0LDOxvBL4kjNzEzW}
pvn.colldge{gfh8UMaLFGfws8-eREMR1jK14c9.0FM0MDOxwCM3kjNzEzW}
pvn.colldge{fgh8VMaLFGfvt8-dREMQ1jL14d9.0FL0MDOxvCM4kjNzDzW}
pvn.colkege{ggg7VMaLEGfws8-dREMQ1jL14d9.0FM0MCOxwBM4kjNzEyW}
pvn.coklege{ggg7VLaLFFevt8-eREMQ1jK14c8.0FM0LDOwvCL4kiNzEzV}
pvn.coklege{gfh8VLaLEFfwt7-dQDMR1jL14d9.0EM0MDOxwCM4kiNzEzV}
pvn.coklefe{ggh8VMaLFFfwt8-eREMR1jL14c9.0FM0MDOxwCM4kjNzEzW}
pvn.cnkldgd{ggh8VMaLFFews8-eRDMR1iK04c9.0FL0MCNwwCM4kjMzEzV}
pvn.bollege{fgh8UMaLFGevs7-eQEMR0jK14d9.0FL0MCOwvBM4kjMzEzW}
pvn.bollege{fgg8VMaKFGfwt8-eRDMQ1jK14d9.0EM0MCNxwBM3kjNzEzW}
pvn.bokldgd{ffh8VMaLFGfvt8-eRDLR1iL04d9.0EL0LDOxwCM3kjNzEzV}
pvm.colkdge{fgh8VLaLFFfwt8-eRELQ1iL14d9.0EL0MCOwwBL4jjNzDyW}
pvm.coklegd{ggg7VLaLFGfws8-eQDMQ0jL14d8.0FM0LDNwvBM4kjNzDzW}
pvm.cnlldfd{ggg7VMaLFGfwt8-eRELR1jL13c9.0FM0MCOxwCM4kjNyEzV}
pvm.cnlkdge{ggg8VLaLEGfwt8-dREMR1iL04d8.0EM0MCNxwCM4kjNzEzW}
own.college{ggh8VMaLFGfwt8-eREMR1iL14d9.0EM0MDOxwCM4kjMzDyW}
own.college{ggh8VMaLFGfwt8-eREMR0jK14d9.0FM0MDOxwBM3kjNzEzV}
own.college{ggh8VLaKFGfwt8-eREMR1jL14d9.0EM0MDOxwBM4kjNzEzV}
own.college{ggh7VMaLEGfwt7-eRDMR1jL14d9.0FM0MDNxwCM4kjNyEzW}
own.college{gfh8ULaLEFfwt8-dREMR1jL14d9.0FM0LDOxwCM4kiNzEzW}
own.colkege{ggh8VLaLFFfvt8-dREMR1jL14c9.0FM0MDOxwCM4kiNzEzW}
own.colkege{fgg7VMaLFGfwt8-dQEMR1iL14c9.0FM0LDOxvCM4kiNzEzW}
own.coklege{ggh8ULaLFFewt7-dRDLR1jK14d9.0FM0LDOxwCM4kjMyEzV}
own.cokkege{ggh8VLaLFGfwt8-eREMR1iL14d9.0FM0MDOxwCM4kjNzEzW}
own.cnllege{ggh8VLaLFFevt8-eRELR1iL04d9.0FM0MDOwwBM4kiMyDyW}
own.cnllegd{ggh8UMaLEGfvt8-dRELR1jL14d9.0FL0MCOxvCM4kjNzDyW}
own.bollege{ggh7UMaLFGfws8-eREMR1jL14d9.0FM0MDNxwCM4kjNzEzW}
own.bollegd{ggh8VMaLFGfvt8-eRDMR1jL04d9.0FM0MDOwvCM4jjNzEyW}
owm.coklegd{ggh7VMaLFGfvt7-eRDMR1jK14d9.0FL0MCNxwBL3kjMzEyV}
owm.cnlldfe{ggh8VLaKEFfwt8-eRELR0jL14d9.0EM0MDNwwBM3jjNzEzV}
owm.cnkldfe{ggg7VMaLFFevt8-eREMR0jK03d8.0EL0MDOxwBM4kjNzDzW}
owm.bokkege{gfh8UMaLFFfvt7-dQELR1jL13d9.0FM0LDNxwCM4kjNzEyW}
ovn.colkege{ggh7UMaLFFfwt8-eREMQ1jK14d9.0FM0MDNxwBM4jjNzEzW}
ovm.collefe{ggh8VLaKFGfwt8-eREMR1jK14d9.0FM0LDOwwCM4kjMyEzW}
ovm.cnlldfe{fgh8VMaLFGfvs8-eRELQ0jK04d9.0EM0MDOxvBM4kjMzEyW}
ovm.bollefd{ggh7VMaKFGewt7-dRDMR1iL04c9.0FL0LDNxvCM4jjNzDzV}
```

The real flag is the first one.

### New Learnings
I learned how to reorder lists with sort. By default sort orders lines alphabetically; using -r reverses that order so the real flag became the first line. I also learned that sort has useful flags.
