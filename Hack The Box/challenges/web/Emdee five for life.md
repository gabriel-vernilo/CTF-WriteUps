# Emdee five for life

## Description
"Can you encrypt fast enough?"


the site has a field that asks for an encrypted text in md5:

![image](https://user-images.githubusercontent.com/53917092/94753540-ddef6a00-0364-11eb-8138-fc5c5895d50b.png)

but when we encrypt and put it manually, it says we are too slow, and gives another text

![image](https://user-images.githubusercontent.com/53917092/94753589-024b4680-0365-11eb-83f7-42173cbbe934.png)

![image](https://user-images.githubusercontent.com/53917092/94753610-198a3400-0365-11eb-8dcb-e5da4829e4ed.png)

we deduce that we have to automate to make it fast

for this I used python3, with the libs : requests, hashlib and bs4

requests to make the connection to the site;
hashlib to encrypt the text in md5;
bs4 to get the text that will be encrypted;

so I wrote the code:

```
import requests
from hashlib import md5
from bs4 import BeautifulSoup

site = "http://docker.hackthebox.eu:31014/"

r = requests.session()
getreq = r.get(site)
h3tag = BeautifulSoup(getreq.text, 'html.parser').find('h3')
Encrypted = md5((str(h3tag)[19:-5]).encode("utf-8")).hexdigest()
data = {'hash':Encrypted}
send = r.post(site,data)
print(send.text)
```

it connects to the site, finds the h3 tag, takes what it contains, encrypts and sends it as data

this returns to the flag