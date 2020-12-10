---
title: STF [Contact Us!]
author: Jason Chua (Coldspot)
date: 2020-12-10 22:09:00 +0800
categories: [CTF, STF]
tags: [mobile, apk, patching]
toc: true
comments: true
excerpt: Looks like Korovax has exposed some development comment lines accidentally. Can you get one of the secrets through this mistake?
---

*60 SOLVES*

*DESCRIPTION*

Looks like Korovax has exposed some development comment lines accidentally. Can you get one of the secrets through this mistake?

*Resources*

[mobile-challenge.apk](https://raw.githubusercontent.com/TeamCookieZ/Stack-the-Flag/main/Mobile/Contact%20Us!/mobile-challenge-cat-2/mobile-challenge.apk)

[apktool](https://ibotpeaches.github.io/Apktool/)



<!--more-->

# Contact Us!

[input-img](/assets/img/blog/STF-Contact-us/1.jpg)

Using jadx, the decompiled code for the contact us form is as shown:

```java
public void onClick(View v) {
    String enteredFlagString = ((EditText) ContactForm.this.findViewById(R.id.editText_name)).getText().toString();
    int toPad = 16 - (enteredFlagString.length() % 16);
    if (toPad != 16) {
        for (int i = 0; i < toPad; i++) {
            enteredFlagString = enteredFlagString + " ";
        }
    }
    int flagStatus = ContactForm.this.retrieveFlag2(enteredFlagString, enteredFlagString.length());
    if (flagStatus == 0) {
        Toast.makeText(ContactForm.this.getApplicationContext(), "The answer is already out if you have been checking something!", 0).show();
    } else if (flagStatus == 2) {
        c.a builder = new c.a(ContactForm.this);
        View view = LayoutInflater.from(ContactForm.this).inflate(R.layout.custom_alert, (ViewGroup) null);
        ((TextView) view.findViewById(R.id.title)).setText("Congrats!");
        ((TextView) view.findViewById(R.id.alert_detail)).setText(new f.a.a.a.a.b.a().a());
        builder.h("Proceed", new DialogInterface$OnClickListenerC0070a());
        builder.f("Close", new b());
        builder.k(view);
        builder.l();
        Toast.makeText(ContactForm.this.getApplicationContext(), "Correct Password!", 0).show();
    } else if (flagStatus == 1) {
        Toast.makeText(ContactForm.this.getApplicationContext(), "Password is wrong!", 0).show();
    } else {
        Toast.makeText(ContactForm.this.getApplicationContext(), "Something is wrong!", 0).show();
    }
}
```

Typing `abracadabra` into the input field will show a toast notification with `The answer is already out if you have been checking something!`. 


I decompiled the apk into smali with the help of apktool. Running `apktool d mobile-challenge.apk` will create a folder with decompiled smali code. By changing the program flow in the smali code by changing line 131 in the file `mobile-challenge/smali/sg/gov/tech/ctf/mobile/Contact/ContactForm$a.smali` to `if-eqz v3, :cond_2` and recompiling the application with `apktool b mobile-challenge`.

Next, to run the apk, we need to sign the apk. By running `keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 10000` and `jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore my-release-key.keystore dist/mobile-challenge.apk alias_name`

After doing so and running the application, and entering `abracadabra`, the application will show the flag.

[flag1-img](/assets/img/blog/STF-Contact-us/2.jpg)

Decompiling the apk with apktool, we will find a `libnative-lib.so` file in `mobile-challenge/lib/x86_64` directory.

Disassembling the shared object with tools like IDA or Ghidra, we can see a function called `Java_sg_gov_tech_ctf_mobile_Contact_ContactForm_retrieveFlag2` which was referenced in the above code snippet `ContactForm.this.retrieveFlag2`. Looking at the function, we can see a comment `Sarah to Samuel: You should see this with the cheat code. Now \'Give me the flag\' will literally give you the flag.` 

Sending `Give me the flag` will also trigger the application to show the flag.

[flag2-img](/assets/img/blog/STF-Contact-us/3.jpg)




More info 
> Ask me on Discord @Coldspot#7033
