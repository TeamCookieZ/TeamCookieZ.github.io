---
title: STF [What is he working on? Some high value project?]
author: Li Zibin (ShallowDream)
date: 2020-12-10 01:48:00 +0800
categories: [CTF, STF]
tags: [OSINT]
toc: true
comments: true
excerpt: The lead Smart Nation engineer is missing! He has not responded to our calls for 3 days and is suspected to be kidnapped! Can you find out some of the projects he has been working on? Perhaps this will give us some insights on why he was kidnapped…maybe some high-value projects! This is one of the latest work, maybe it serves as a good starting point to start hunting. Flag is the repository name!
---

*103 SOLVES*

*Description*

The lead Smart Nation engineer is missing! He has not responded to our calls for 3 days and is suspected to be kidnapped! Can you find out some of the projects he has been working on? Perhaps this will give us some insights on why he was kidnapped…maybe some high-value projects! This is one of the latest work, maybe it serves as a good starting point to start hunting.

Flag is the repository name!

*Document provided*

[Link](https://www.developer.tech.gov.sg/communities/events/stack-the-flags-2020)

*Tools used*

- Google Chrome

<!--more-->

# Evaluating current resources

We were given a link that links to the Developer Portal for STF CTF.

`https://www.developer.tech.gov.sg/communities/events/stack-the-flags-2020`

![upload-image](/assets/img/blog/STF-What-is-he-working-on/1.png)

Nothing was found on the page itself, so I went to take a look at the source code.

As I look through the source code, some suspicious comments were found.

`<!-- Will fork to our gitlab - @joshhky -->`

![upload-image](/assets/img/blog/STF-What-is-he-working-on/2.png)

With this information, we can now proceed to Joshhky's Gitlab to dig out more information!

We can go to his Gitlab by appending his Gitlab handle to gitlab.com

`https://gitlab.com/joshhky`


# Digging through Gitlab

After visiting his Gitlab, I went straight to his activity to find any suspicious actions.

Most of the activities were project creation and branch creation, but there was one activity that he committed to korovax-employee-wiki.

![upload-image](/assets/img/blog/STF-What-is-he-working-on/3.png)

Moving into the commit, we can see his commits on README.md, with one line saying: `Todo: ... The employee wiki will list what each employee is responsible for, eg, Josh will be in charge of the krs-admin-portal`

Based on the decription of the question, the flag should be a repo name, and the Todo links back to a project that he is **working** on, as suggested in the description.


![upload-image](/assets/img/blog/STF-What-is-he-working-on/4.png)

The final flag is `govtech-csg{krs-admin-portal}`

# Thoughts

It was a rather simple challenge with straight forward description and hints that leads to the flag.
