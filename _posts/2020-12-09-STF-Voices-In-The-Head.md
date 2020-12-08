---
title: STF [Voices in the head]
author: Li Zibin (ShallowDream)
date: 2020-12-09 01:48:00 +0800
categories: [CTF, STF]
tags: [forensics]
toc: true
comments: true
excerpt: We found a voice recording in one of the forensic images but we have no clue what's the voice recording about. Are you able to help?
---

*40 SOLVES*

*Description*

We found a voice recording in one of the forensic images but we have no clue what's the voice recording about. Are you able to help?

*Document provided*

![forensics-challenge-2.wav](https://github.com/TeamCookieZ/Stack-the-Flag/raw/main/Forensics/Voices%20in%20the%20head/forensics-challenge-2.wav)

*Tools used*

Sonic Visualizer, Xiao Steganography

<!--more-->

# Evaluating current resources

Before we start, lets check out the relevant information for this challenge file. 

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/1.png)

Running binwalk on the file, nothing suspicious.

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/2.png)

Playing the file sounds like someone wiping the window for 5 seconds, but from here, we can make some educated guesses.


# Guessing what can be hidden

Usually, when given a .wav or any sound extension files, we can find hidden stuffs in these two areas:

#### Sound
The sound it plays usually gives off what it was encoded with (eg. DTMF, Morse Code etc.). However, in this file, the sound it plays does not sound like any encoding methods that I know of.

#### Spectrogram
A spectrogram is a visual way of representing the signal strength, or "loudness" of signal over time at various frequencies present in a particular waveform. It can be viewed with tools like Audacity, Sonic Visualizer or even online tools.

CTF challenges ***LOVE*** to write stuff on spectrogram.

This is a snip of the spectrogram from the challenge file using Sonic Visualizer.

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/3.png)


# Diving into spectrogram

It looks like there are words written onto the spectrogram, but before that let us fix the view by pressing *F* to zoom to fit (~no~ ~memes~ ~intented~), so we can see the words clearly.

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/4.png)

`aHR0cHM6Ly9wYXN0ZWJpbi5jb20vakVUajJ1VWI=`

We get a string of text that looks like a base64 encoded string.

After decoding, it leads us to a [pastebin url](https://pastebin.com/jETj2uUb).

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/5.png)

The contents in the pastebin were texts in [Brainfuck](https://en.wikipedia.org/wiki/Brainfuck#:~:text=Brainfuck%20is%20an%20esoteric%20programming,to%20challenge%20and%20amuse%20programmers.) language.

`++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>>++++++++++++++++.------------.+.++++++++++.----------.++++++++++.-----.+.+++++..------------.---.+.++++++.-----------.++++++.`

Using a online decoder, the decrypted text happens to be `thisisnottheflag`.

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/6.png)

# Dead end?

After getting `thisisnottheflag`, I thought I went down a rabbit hole set by the creators and was lost. In the end, I opened a ticket to ask if this was intended.

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/7.png)

However it seems like this was a part of the challenge, but I had no clue on whats the next step, and so is everyone else in this CTF.

Till Day 2 (~one~ ~day~ ~before~ ~the~ ~end~ ~of~ ~the~ ~CTF~), **no one** solved the challenge and people are starting to go mad.

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/8.png)

# bbbb's Saving Grace

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/9.png)

On Day 3 morning, an addendum was added to the challenge description, which basically gave everyone a free fint and help them go through the tough times of having voices in their head.

The hint reads
`Xiao wants to help. Will you let him help you?`

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/10.png) :~me?~

This immediately got me searching for steganography resources related to Xiao, and I ended up with a tool called Xiao Steganography.

# Solving

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/11.png)
![upload-image](/assets/img/blog/STF-Voices-In-The-Head/12.png)

After installing Xiao Steganography and loading the challenge file in, we get a prompt suggesting a zip file embedded inside the challenge file and requires a password to be extracted out from the challenge file.

Linking back, we got a somewhat password looking string back when decoding Brainfuck, and `thisisnottheflag` unlockes the file!

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/13.png)

The extracted zip file contains a document file, but requires a password for it to be extracted. Using `thisisnottheflag` does not unlock the file.

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/14.png)

Since it is document file, I pulled the zip file back into my Kali Linux and ran strings on the zip file, which yields me the flag!

![upload-image](/assets/img/blog/STF-Voices-In-The-Head/15.png)

`Flag: govtech-csg{Thisisn0ty3tthefl@g}`

# Thoughts

It was a very fustrating challenge when I was stuck after decoding `thisisnottheflag`. Tried everything like changing file headers, binwalk, steghide, but none of them seems to work. Everything went smooth sailing only after the free hint was given out on Day 3.


~PS.~ ~~Apparently Xiao Steganography was hinted in the challenge title, Xiao being the [Singlish equivalent](http://www.singlish.net/siao/) of being **crazy**, which hence suggesting having Voices in the Head.~~