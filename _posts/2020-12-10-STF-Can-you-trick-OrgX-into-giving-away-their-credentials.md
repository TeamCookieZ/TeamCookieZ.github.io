---
title: STF [Can you trick OrgX into giving away their credentials?]
author: Li Zibin (ShallowDream)
date: 2020-12-10 01:48:00 +0800
categories: [CTF, STF]
tags: [Social Engineering, email, sitemap]
toc: true
comments: true
excerpt: With the information gathered, figure out who has access to the key and contact the person.
---

*14 SOLVES*

*Description*

With the information gathered, figure out who has access to the key and contact the person.

*Document provided*

- None

*Tools used*

- Google Chrome, Outlook

<!--more-->

# Evaluating current resources

Linking back to the previous previous challenge ([Who are the possible kidnappers?)](https://team.nullsecsig.com/posts/STF-Who-are-the-possible-kidnappers), we know that the organization name is Korovax and they have a internal social media page.

![upload-image](/assets/img/blog/STF-Can-you-trick-OrgX-into-giving-away-their-credentials/1.png)

Clicking onto the link, it leads us to Korovax's internal Facebook page.

`fb.korovax.org`

and I was able to register an account without verification.

![upload-image](/assets/img/blog/STF-Can-you-trick-OrgX-into-giving-away-their-credentials/2.png)

# Korovax's Facebook

As I click onto my profile, I realised there were IDs appended to the back of the profile, with mine currently being 3401.

![upload-image](/assets/img/blog/STF-Can-you-trick-OrgX-into-giving-away-their-credentials/3.png)

I thought that the users might be ID-ed according to registration time, so I cycled through the user IDs starting from 0 and the first 13 IDs (if I recalled correctly) belongs to Korovax employees.

User ID 5, William Birkin had a interesting, or rather informative feed, spitting out some emails that sounded like a tech-support.

`ictadmin@korovax.org`

![upload-image](/assets/img/blog/STF-Can-you-trick-OrgX-into-giving-away-their-credentials/4.png)

# Emailing ictadmin

Now that's interesting. From the Korovax's blog, a post suggests that the ictadmin for Korovax might be a automated helpdesk, so I tried my luck and emailed him random stuff.

![upload-image](/assets/img/blog/STF-Can-you-trick-OrgX-into-giving-away-their-credentials/5.png)

To my surprise, he actually emailed me back!

![upload-image](/assets/img/blog/STF-Can-you-trick-OrgX-into-giving-away-their-credentials/6.png)

Linking back to the category of this challenge, it seems like we need a passphrase to trigger an automated reply from ictadmin, so I went back and dig into the sitemap again.

# Finding passphrase

After clicking into multiple links in the sitemap (can be found in previous challenge), I came across the page `https://csgctf.wordpress.com/never-gonna/` which had IT highlighted in **bold**. So I had to assume that this have something to do with triggering the automated reply from ictadmin.

The link had `never-gonna`, which is a song reference to `Rick Astley - Never Gonna Give You Up`. It is also a widely known [internet meme](https://knowyourmeme.com/memes/rickroll) called Rickrolling.

With this idea in mind, I quickly realised that the first letter of each line in this post is `R I C K R O L L`.

![upload-image](/assets/img/blog/STF-Can-you-trick-OrgX-into-giving-away-their-credentials/7.png)

I tried emailing `ictadmin@korovax.org` once again with this passphrase in the email title and body.

![upload-image](/assets/img/blog/STF-Can-you-trick-OrgX-into-giving-away-their-credentials/8.png)

And almost instantly, I received a email of congratulations.

![upload-image](/assets/img/blog/STF-Can-you-trick-OrgX-into-giving-away-their-credentials/9.png)

And we got our result.

The final flag is `govtech-csg{CE236F40A35E48F51E921AD5D28CF320265F33B3}`

# Thoughts

This was rather easy for me to solve. In fact, I solve this before I solved [Who are the possible kidnappers?](https://team.nullsecsig.com/posts/STF-Who-are-the-possible-kidnappers) since there were a lot of information on Korovax's blog and internal social media. At one point, I thought the passphrase was hidden in the password locked blog post, but alas it wasn't!