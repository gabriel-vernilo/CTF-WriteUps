# Fuzzy

## Description

"We have gained access to some infrastructure which we believe is connected to the internal network of our target. We need you to help obtain the 
administrator password for the website they are currently developing"

### First Recognition

for the whole fuzzing process (process of finding pages and parameters using a list of words) I will use a tool called dirbuster

![image](https://user-images.githubusercontent.com/53917092/94797179-27b47080-03b6-11eb-9b41-e532d8ceac69.png)

with the checkbox "Be recursive" marked, it will find :

* /index.html
* /css/
* /js/
* /api/
* /api/index.html
* /api/action.php

inside css js folders you will find more things, but those don't matter

### /api/action.php

this page says :

Error: Parameter not set

so we have to find out what parameter it expects in the url

for this we will use the url fuzz option of the dirbuster

![image](https://user-images.githubusercontent.com/53917092/94798852-94c90580-03b8-11eb-9323-18facd4482a2.png)

so we discovered that the expected parameter was "reset"

the page

/api/action.php?reset=

contains the message:

"Error: Account ID not found"

then we run the dirbuster again with the url fuzz option, but now using the correct parameter

![image](https://user-images.githubusercontent.com/53917092/94799326-5253f880-03b9-11eb-9e53-9f1558e4365e.png)

analyzing the responses we see that when we put 20 in the "reset" parameter we have a different response

checking the page with the url /api/action.php?reset=20

it contains our flag

