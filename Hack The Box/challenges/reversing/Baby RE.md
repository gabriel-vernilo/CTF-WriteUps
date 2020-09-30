# Baby RE

## Description 

"Show us your basic skills! (P.S. There are 4 ways to solve this, are you willing to try them all?)"

and we have a file, which by unzipping we give a file without extension called "baby"

seeing the strings of this file we see interesting thing, like

```
HTB{B4BYH
_R3V_TH4H
TS_Ef

"Don't run "strings" on this challenge, that is not the way!!!!"

insert key:
abcde122313
```
but for me what most caught my attention were the following strings

```
puts
stdin
strcmp
GCC: (Debian 9.2.1-8) 9.2.1 20190909
baby.c
```
because it indicates that this file is a file that can be decompiled into a C file

for this I used the reverse engineering program called Ghidra

after decompiling and recompiling this program in a C code, we have this:

![image](https://user-images.githubusercontent.com/53917092/94746476-2a31ae80-0353-11eb-8c51-086acb58a3e1.png)


and passing this strings from hexadecimal to ascii

![image](https://user-images.githubusercontent.com/53917092/94746518-46cde680-0353-11eb-9f91-5b5d44e6d168.png)


we have :

![image](https://user-images.githubusercontent.com/53917092/94746616-83014700-0353-11eb-8d95-19820f3428b9.png)


is strange because it refers to memory addresses, that is, these strings are backwards, but in pairs

example : 0x7d5a is   0x5a 0x7d

then fixing, we have:

```
0x594234427b425448
0x3448545f5633525f
0x455f5354
0x7d5a
```

==>

```
48 54 42 7b 42 34 42 59
5f 52 33 56 5f 54 48 34
54 53 5f 45
5a 7d
```

now, if we convert this to ascii, we have the right flag