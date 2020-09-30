# Bank Heist

## Description

"You get to the scene of a bank heist and find that you have caught one person. Under further analysis of the persons flip phone you see a message that seems suspicious. Can you figure out what the message to put this guy in jail?"

and we have a file, which by unzipping we give a text file that contains the following message

```
"444333 99966688 277733 7773323444664 84433 22244474433777, 99966688 277733 666552999. 99966688777 777744277733 666333 84433 443344477778 4447777 44466 99966688777 4466688777733. 84433 5533999 8666 84433 55566622255 4447777 22335556669. 4666 8666 727774447777.

47777888 995559888 4555 47777888 44999988 666555997 : 8555444888477744488866888648833369!!"
```

After a little analysis, I realized that it was a message typed into these phones:

![image](https://user-images.githubusercontent.com/53917092/94738785-4c70ff80-0346-11eb-82fc-d719aa74fc5f.png)

decoding, we have :

```
"IF YOU ARE READING THE CIPHER, YOU ARE OKAY. YOUR SHARE OF THE HEIST IS IN YOUR HOUSE. THE KEY TO THE LOCK IS BELOW. GO TO PARIS.

GSV XLWV GL GSV HZU OLXP : TLIVGRIVNVMGUFMW!!"
```
in this last part, we have one more encoded phrase, testing some cryptographs, I reached the caesar cipher, (that I have already programmed an encoder and decoder, look at my repositories here at github), and when I tried with 25 of shift, I got the answer.

![image](https://user-images.githubusercontent.com/53917092/94739321-3283ec80-0347-11eb-9dda-40cb04c3e8dc.png)

"GSV XLWV GL GSV HZU OLXP : TLIVGRIVNVMGUFMW!!"  -->  "HE CODE TO THE SAF LOCK : GORETIREMENTFUND!!"
