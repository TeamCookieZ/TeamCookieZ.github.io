---
title: STF [Where's the flag?]
author: Lim Kai Xian (AxiaMil)
date: 2020-12-11 03:03:00 +0800
categories: [CTF, STF]
tags: [png, forensic]
toc: true
comments: true
excerpt: There's plenty of space to hide flags in our spacious office. Let's see if you can find it!
---

*35 SOLVES*

*DESCRIPTION*

There's plenty of space to hide flags in our spacious office. Let's see if you can find it!  

![upload-image](/assets/img/blog/STF-Where-is-the-flag/1.png)

![misc-challenge-7.png](https://github.com/TeamCookieZ/Stack-the-Flag/blob/main/Miscellaneous/Where%27s%20the%20flag/misc-challenge-7.png?raw=true)

Downloading the file from the challenge i was presented with a png file.  
I firstly check if it is really a png file using the command `file`

![upload-image](/assets/img/blog/STF-Where-is-the-flag/2.png)

Ok! it is a png file, lets check it out.  

![upload-image](/assets/img/blog/STF-Where-is-the-flag/3.png)

Oof, there seems to be an error with the png file. I tried using gimp as it was less strict when viewing images.  

![upload-image](/assets/img/blog/STF-Where-is-the-flag/4.png)

Okay, it work! The image seems to be just a ordinary image of govtech work place. 
The image did not give us much information on what to work on next so lets do run some basic forensic tool for more information like
binwalk, pngcheck, exiftool, stegohide and changing the colour palette using this [amazing online tool](https://stegonline.georgeom.net/upload).
After running all the tools gave no additional information to work on. I decided to look into the hex itself. using the tool called `bless`, 
I scan through the hex and found something very weird at the end of the file.  

![upload-image](/assets/img/blog/STF-Where-is-the-flag/5.png)  

Going to [wikipedia](https://en.wikipedia.org/wiki/Portable_Network_Graphics), you would know that that part of the file is called a zTxt which is a compressed text that works the same as tEXt in png.
To extract the zTxt, i used [dcode.fr](https://www.dcode.fr/png-chunks) and input it into a file, however you can just copy it using the hex editor you are using.  

After extracting i was quite clueless on what to do next? It just look like gibberish???  

![upload-image](/assets/img/blog/STF-Where-is-the-flag/6.png)  

 Trying my luck i just copied the entire text and base64 decode it. To my surprise something interesting came up!!  

 ![upload-image](/assets/img/blog/STF-Where-is-the-flag/7.png)  

 Oh yes, it is the hex of the PNG file!

 Using [dcode.fr](https://www.dcode.fr/base-64-encoding) again, i threw in the long ass base64 code and chose `file to download` as the result format.  

 ![upload-image](/assets/img/blog/STF-Where-is-the-flag/8.png)  

 Getting the file, i changed the file to a png using the mv command 
 ```
 $ mv dcode-data.txt file.png
 ```
 
 This is the new png i got

 ![upload-image](/assets/img/blog/STF-Where-is-the-flag/9.png)  

 Running the same tools i did before i was able to get the flag through changing the colour palatte using this [amazing online tool](https://stegonline.georgeom.net/upload).
 Pressing randomize palette i was able to get the flag hidden in the pole of the flag 

![upload-image](/assets/img/blog/STF-Where-is-the-flag/10.png)

Zooming and rotating the image i got

![upload-image](/assets/img/blog/STF-Where-is-the-flag/11.png)

hence, i was able to get the flag `govtech-csg{f1agcepti0N}`

# Thoughts

This challenge was pretty easy, however i was not able to identify the zTxt was a base64 encoded text hence i was not able to continue forward and when to run more stego tools