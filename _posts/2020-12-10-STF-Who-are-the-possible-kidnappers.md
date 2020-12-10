---
title: STF [Who are the possible kidnappers?]
author: Li Zibin (ShallowDream)
date: 2020-12-10 01:48:00 +0800
categories: [CTF, STF]
tags: [OSINT]
toc: true
comments: true
excerpt: Perform OSINT to gather information on the organisation’s online presence. Start by identifying a related employee and obtain more information. Information are often posted online to build the organization's or the individual's online presence (i.e. blog post). Flag format is the name of the employee and the credentials, separated by an underscore. For example, the name is Tina Lee and the credentials is MyPassword is s3cure. The flag will be govtech-csg{TinaLee_MyPassword is s3cure}

---

*16 SOLVES*

*Description*

Perform OSINT to gather information on the organisation’s online presence. Start by identifying a related employee and obtain more information. Information are often posted online to build the organization's or the individual's online presence (i.e. blog post). Flag format is the name of the employee and the credentials, separated by an underscore. For example, the name is Tina Lee and the credentials is MyPassword is s3cure. The flag will be govtech-csg{TinaLee_MyPassword is s3cure}

Addendum:
- Look through the content! Have you looked through ALL the pages? If you believe that you have all the information required, take a step back and analyse what you have.
- In Red Team operations, it is common for Red Team operators to target the human element of an organisation. Social medias such as "Twitter" often have information which Red Team operators can use to pivot into the organisation. Also, there might be hidden portal(s) that can be discovered through "sitemap(s)"?

I guess if you can log in with the password, then you should look at the flag format again!

Note: engaging/contacting Ms. Miller is not in scope for this ctf.

*Document provided*

- None

*Tools used*

- Google Chrome

<!--more-->

# Evaluating current resources

Linking back to the previous previous challenge ([What is he working on? Some high value project?)](https://team.nullsecsig.com/posts/STF-What-is-he-working-on), we know that the organization name is Korovax.

The description also hints us that the we might need to find a blog/blog post regarding Korovax. Hence, we can format our Google search like this:

`Korovax "blog"`

which forces Google to include the term **blog** in their search result.

This gives us this result.

![upload-image](/assets/img/blog/STF-Who-are-the-possible-kidnappers/1.png)

# Korovax Blog

![upload-image](/assets/img/blog/STF-Who-are-the-possible-kidnappers/2.png)

Clicking into the posts yielded me with nothing. So I went about checking the sitemap and robots.txt to see if there are any other hidden pages.

![upload-image](/assets/img/blog/STF-Who-are-the-possible-kidnappers/3.png)

![upload-image](/assets/img/blog/STF-Who-are-the-possible-kidnappers/4.png)

A lot of interesting pages not shown in the blog showed up, and after checking each and every link, the one the was most useful to us was:

`https://csgctf.wordpress.com/oh-ho/`

![upload-image](/assets/img/blog/STF-Who-are-the-possible-kidnappers/5.png)

The post mentioned about archived tweets, so my first thought was Twitter, but wasn't sure who I should look out for.

I then headed to the Teams tab to see who were in the Team, and gave me the following personnels: `Oswell E Spencer, Sarah Miller and 
Samuel the Dog`.

![upload-image](/assets/img/blog/STF-Who-are-the-possible-kidnappers/6.png)

# Twitter hunting

My best bet was Sarah Miller, since searching Oswell E Spencer gives me **so** many Resident Evil results.

![upload-image](/assets/img/blog/STF-Who-are-the-possible-kidnappers/7.png)

There were also a lot of Sarah Millers on Twitter, after looking through most of the Sarah Millers, the most relevant Sarah Miller I've found was @scba.

![upload-image](/assets/img/blog/STF-Who-are-the-possible-kidnappers/8.png)

Remember she said archived tweets and the keywords `blue something communications`? It seems like we are missing a word here.

So, we can utilise Twitter's advance search function to search our keywords from a specific user.

![upload-image](/assets/img/blog/STF-Who-are-the-possible-kidnappers/9.png)

![upload-image](/assets/img/blog/STF-Who-are-the-possible-kidnappers/10.png)

And we got our result.

![upload-image](/assets/img/blog/STF-Who-are-the-possible-kidnappers/11.png)

Back to our flag format, with the information we have now, the final flag is `govtech-csg{SarahMiller_Blue sky communications}`

# Thoughts

A lot of effort was put into this challenge as the search results were too much to handle. I would call myself lucky to bump into @scba in the first page of the Google Search.