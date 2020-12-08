---
title: STF [An invitation]
author: Jason Chua (Coldspot)
date: 2020-12-08 17:50:28 +0800
categories: [CTF, STF]
tags: [javascript, reverse]
toc: true
comments: true
---

*34 SOLVES*

*DESCRIPTION*

We want you to be a member of the Cyber Defense Group! Your invitation has been encoded to avoid being detected by COViD's sensors. Decipher the invitation and join in the fight!

*Resources*

index.html
```html
<!doctype html>
<html lang="en">
    <head>
        <!-- Required meta tags -->
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

        <!-- Bootstrap CSS -->
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css" integrity="sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2" crossorigin="anonymous">

        <title>Hello, world!</title>
    </head>
    <body>
        <div class="container">
            <br />
            <div class="custom1"></div>
            <div class="custom2"></div>
            <div class="custom3"></div>
            <canvas class="Gl" id="glglglgl" width="1" height="1" shade="e" type="l"></canvas>
            <br />
        </div>
        <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ho+j7jyWK8fNQe+A12Hb8AhRq26LrZ/JpcUGGOn+Y7RsweNrtN/tE3MoK7ZeZDyx" crossorigin="anonymous"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/raphael/2.2.7/raphael.min.js"></script>
        <script src="jquery-led.js"></script>
        <script src="invite.js"></script>
    </body>
</html>
```

```js
var _0x3f3a=["\x2E\x47","\x71\x75\x65\x72\x79\x53\x65\x6C\x65\x63\x74\x6F\x72","\x77\x65\x62\x67\x6C","\x67\x65\x74\x43\x6F\x6E\x74\x65\x78\x74","\x63\x6C\x65\x61\x72\x43\x6F\x6C\x6F\x72","\x63\x6C\x65\x61\x72","\x73\x68\x61\x64\x65","\x67\x65\x74\x41\x74\x74\x72\x69\x62\x75\x74\x65","\x74\x79\x70\x65","\x73\x6C\x69\x63\x65","\x69\x64","\x4B\x47","\x7C\x7C\x7C\x7C\x7C\x7C\x66\x75\x6E\x63\x74\x69\x6F\x6E\x7C\x76\x61\x72\x7C\x7C\x68\x68\x68\x7C\x7C\x7C\x7C\x66\x6F\x72\x7C\x63\x68\x61\x72\x43\x6F\x64\x65\x41\x74\x7C\x69\x66\x7C\x6C\x65\x6E\x67\x74\x68\x7C\x65\x65\x65\x7C\x7C\x75\x75\x75\x7C\x7C\x6D\x6D\x6D\x7C\x7C\x7C\x63\x75\x73\x74\x6F\x6D\x7C\x66\x72\x6F\x6D\x43\x68\x61\x72\x43\x6F\x64\x65\x7C\x53\x74\x72\x69\x6E\x67\x7C\x76\x76\x76\x7C\x7C\x67\x67\x67\x7C\x6C\x6F\x63\x61\x74\x69\x6F\x6E\x7C\x63\x61\x74\x4C\x45\x44\x7C\x74\x79\x70\x65\x7C\x7C\x63\x6F\x6C\x6F\x72\x7C\x7C\x72\x6F\x75\x6E\x64\x65\x64\x7C\x66\x6F\x6E\x74\x5F\x74\x79\x70\x65\x7C\x62\x61\x63\x6B\x67\x72\x6F\x75\x6E\x64\x5F\x63\x6F\x6C\x6F\x72\x7C\x65\x30\x65\x30\x65\x30\x7C\x73\x69\x7A\x65\x7C\x72\x65\x74\x75\x72\x6E\x7C\x7A\x7A\x7A\x7C\x46\x46\x30\x30\x30\x30\x7C\x76\x61\x6C\x75\x65\x7C\x73\x65\x65\x64\x7C\x79\x79\x79\x7C\x72\x72\x72\x7C\x7C\x6F\x6F\x6F\x7C\x73\x6C\x69\x63\x65\x7C\x74\x74\x74\x7C\x66\x61\x6C\x73\x65\x7C\x77\x69\x6E\x64\x6F\x77\x7C\x65\x6C\x73\x65\x7C\x79\x6F\x75\x7C\x69\x69\x69\x7C\x6C\x65\x74\x7C\x59\x4F\x55\x7C\x7C\x63\x6F\x6D\x70\x61\x72\x65\x7C\x30\x78\x66\x66\x7C\x7C\x7C\x32\x33\x7C\x72\x65\x7C\x68\x6F\x73\x74\x6E\x61\x6D\x65\x7C\x63\x6F\x6E\x73\x6F\x6C\x65\x7C\x7C\x7C\x35\x37\x7C\x70\x72\x6F\x74\x6F\x63\x6F\x6C\x7C\x66\x69\x6C\x65\x7C\x35\x34\x7C\x6C\x6F\x67\x7C\x6D\x61\x78\x7C\x4D\x61\x74\x68\x7C\x39\x38\x7C\x72\x65\x71\x75\x65\x73\x74\x41\x6E\x69\x6D\x61\x74\x69\x6F\x6E\x46\x72\x61\x6D\x65\x7C\x74\x72\x75\x65\x7C\x30\x42\x42\x7C\x30\x30\x7C\x38\x38\x7C\x30\x39\x7C\x30\x46\x5A\x7C\x30\x32\x7C\x30\x44\x7C\x30\x36\x48\x44\x7C\x30\x33\x53\x7C\x33\x31\x7C\x67\x65\x74\x7C\x6E\x65\x77\x7C\x49\x6D\x61\x67\x65\x7C\x4F\x62\x6A\x65\x63\x74\x7C\x64\x65\x66\x69\x6E\x65\x50\x72\x6F\x70\x65\x72\x74\x79\x7C\x69\x64\x7C\x75\x6E\x65\x73\x63\x61\x70\x65\x7C\x69\x6E\x76\x69\x74\x65\x64\x7C\x32\x30\x30\x30\x7C\x70\x61\x74\x68\x6E\x61\x6D\x65\x7C\x63\x6F\x6E\x73\x74\x7C\x65\x63\x68\x7C\x7C\x73\x65\x74\x54\x69\x6D\x65\x6F\x75\x74\x7C\x57\x41\x4E\x54\x7C\x57\x45\x7C\x63\x75\x73\x74\x6F\x6D\x33\x7C\x63\x75\x73\x74\x6F\x6D\x32\x7C\x49\x4E\x56\x49\x54\x45\x44\x7C\x52\x45\x7C\x63\x75\x73\x74\x6F\x6D\x31\x7C\x64\x65\x62\x75\x67\x67\x65\x72\x7C\x31\x30\x30\x30\x7C\x69\x6E\x76\x69\x74\x65\x7C\x74\x68\x65\x7C\x61\x63\x63\x65\x70\x74\x69\x6E\x67\x7C\x61\x6C\x65\x72\x74\x7C\x54\x68\x61\x6E\x6B\x7C\x69\x6E\x64\x65\x78\x4F\x66\x7C\x67\x6F\x7C\x31\x31\x38\x7C\x33\x56\x33\x6A\x59\x61\x6E\x42\x70\x66\x44\x71\x35\x51\x41\x62\x37\x4F\x4D\x43\x63\x54\x7C\x6C\x65\x61\x48\x56\x57\x61\x57\x4C\x66\x68\x6A\x34\x7C\x61\x74\x6F\x62","\x74\x6F\x53\x74\x72\x69\x6E\x67","\x72\x65\x70\x6C\x61\x63\x65","\x78\x3D\x5B\x30\x2C\x30\x2C\x30\x5D\x3B\x31\x43\x20\x59\x3D\x28\x61\x2C\x62\x29\x3D\x3E\x7B\x56\x20\x73\x3D\x27\x27\x3B\x64\x28\x56\x20\x69\x3D\x30\x3B\x69\x3C\x31\x65\x2E\x31\x64\x28\x61\x2E\x67\x2C\x62\x2E\x67\x29\x3B\x69\x2B\x2B\x29\x7B\x73\x2B\x3D\x71\x2E\x70\x28\x28\x61\x2E\x65\x28\x69\x29\x7C\x7C\x30\x29\x5E\x28\x62\x2E\x65\x28\x69\x29\x7C\x7C\x30\x29\x29\x7D\x46\x20\x73\x7D\x3B\x66\x28\x75\x2E\x31\x39\x3D\x3D\x27\x31\x61\x3A\x27\x29\x7B\x78\x5B\x30\x5D\x3D\x31\x32\x7D\x53\x7B\x78\x5B\x30\x5D\x3D\x31\x38\x7D\x66\x28\x59\x28\x52\x2E\x75\x2E\x31\x34\x2C\x22\x54\x27\x31\x33\x20\x31\x7A\x21\x21\x21\x22\x29\x3D\x3D\x31\x79\x28\x22\x25\x31\x45\x25\x31\x6A\x25\x31\x71\x25\x31\x37\x25\x31\x70\x25\x31\x6F\x25\x31\x6E\x25\x31\x6D\x25\x31\x6C\x25\x31\x69\x40\x4D\x22\x29\x29\x7B\x78\x5B\x31\x5D\x3D\x31\x6B\x7D\x53\x7B\x78\x5B\x31\x5D\x3D\x31\x72\x7D\x36\x20\x4B\x28\x29\x7B\x37\x20\x6A\x3D\x51\x3B\x37\x20\x47\x3D\x31\x74\x20\x31\x75\x28\x29\x3B\x31\x76\x2E\x31\x77\x28\x47\x2C\x27\x31\x78\x27\x2C\x7B\x31\x73\x3A\x36\x28\x29\x7B\x6A\x3D\x31\x68\x3B\x78\x5B\x32\x5D\x3D\x31\x62\x7D\x7D\x29\x3B\x31\x67\x28\x36\x20\x58\x28\x29\x7B\x6A\x3D\x51\x3B\x31\x35\x2E\x31\x63\x28\x22\x25\x63\x22\x2C\x47\x29\x3B\x66\x28\x21\x6A\x29\x7B\x78\x5B\x32\x5D\x3D\x31\x66\x7D\x7D\x29\x7D\x3B\x4B\x28\x29\x3B\x36\x20\x4E\x28\x4A\x29\x7B\x37\x20\x6D\x3D\x5A\x3B\x37\x20\x61\x3D\x31\x31\x3B\x37\x20\x63\x3D\x31\x37\x3B\x37\x20\x7A\x3D\x4A\x7C\x7C\x33\x3B\x46\x20\x36\x28\x29\x7B\x7A\x3D\x28\x61\x2A\x7A\x2B\x63\x29\x25\x6D\x3B\x46\x20\x7A\x7D\x7D\x36\x20\x55\x28\x68\x29\x7B\x50\x3D\x68\x5B\x30\x5D\x3C\x3C\x31\x36\x7C\x68\x5B\x31\x5D\x3C\x3C\x38\x7C\x68\x5B\x32\x5D\x3B\x4C\x3D\x4E\x28\x50\x29\x3B\x74\x3D\x52\x2E\x75\x2E\x31\x42\x2E\x4F\x28\x31\x29\x3B\x39\x3D\x22\x22\x3B\x64\x28\x69\x3D\x30\x3B\x69\x3C\x74\x2E\x67\x3B\x69\x2B\x2B\x29\x7B\x39\x2B\x3D\x71\x2E\x70\x28\x74\x2E\x65\x28\x69\x29\x2D\x31\x29\x7D\x72\x3D\x31\x5A\x28\x22\x31\x58\x2F\x2F\x6B\x2F\x31\x59\x3D\x22\x29\x3B\x6C\x3D\x22\x22\x3B\x66\x28\x39\x2E\x4F\x28\x30\x2C\x32\x29\x3D\x3D\x22\x31\x56\x22\x26\x26\x39\x2E\x65\x28\x32\x29\x3D\x3D\x31\x57\x26\x26\x39\x2E\x31\x55\x28\x27\x31\x44\x2D\x63\x27\x29\x3D\x3D\x34\x29\x7B\x64\x28\x69\x3D\x30\x3B\x69\x3C\x72\x2E\x67\x3B\x69\x2B\x2B\x29\x7B\x6C\x2B\x3D\x71\x2E\x70\x28\x72\x2E\x65\x28\x69\x29\x5E\x4C\x28\x29\x29\x7D\x31\x53\x28\x22\x31\x54\x20\x54\x20\x64\x20\x31\x52\x20\x31\x51\x20\x31\x50\x21\x5C\x6E\x22\x2B\x39\x2B\x6C\x29\x7D\x7D\x64\x28\x61\x3D\x30\x3B\x61\x21\x3D\x31\x4F\x3B\x61\x2B\x2B\x29\x7B\x31\x4E\x7D\x24\x28\x27\x2E\x31\x4D\x27\x29\x2E\x76\x28\x7B\x77\x3A\x27\x6F\x27\x2C\x79\x3A\x27\x23\x48\x27\x2C\x43\x3A\x27\x23\x44\x27\x2C\x45\x3A\x31\x30\x2C\x41\x3A\x35\x2C\x42\x3A\x34\x2C\x49\x3A\x22\x20\x57\x27\x31\x4C\x20\x31\x4B\x21\x20\x22\x7D\x29\x3B\x24\x28\x27\x2E\x31\x4A\x27\x29\x2E\x76\x28\x7B\x77\x3A\x27\x6F\x27\x2C\x79\x3A\x27\x23\x48\x27\x2C\x43\x3A\x27\x23\x44\x27\x2C\x45\x3A\x31\x30\x2C\x41\x3A\x35\x2C\x42\x3A\x34\x2C\x49\x3A\x22\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x22\x7D\x29\x3B\x24\x28\x27\x2E\x31\x49\x27\x29\x2E\x76\x28\x7B\x77\x3A\x27\x6F\x27\x2C\x79\x3A\x27\x23\x48\x27\x2C\x43\x3A\x27\x23\x44\x27\x2C\x45\x3A\x31\x30\x2C\x41\x3A\x35\x2C\x42\x3A\x34\x2C\x49\x3A\x22\x20\x20\x20\x31\x48\x20\x31\x47\x20\x57\x21\x20\x20\x22\x7D\x29\x3B\x31\x46\x28\x36\x28\x29\x7B\x55\x28\x78\x29\x7D\x2C\x31\x41\x29\x3B","\x5C\x77\x2B","\x73\x68\x69\x66\x74","\x70\x75\x73\x68","\x30\x78\x32","\x7C","\x73\x70\x6C\x69\x74","\x30\x78\x34","","\x66\x72\x6F\x6D\x43\x68\x61\x72\x43\x6F\x64\x65","\x30\x78\x30","\x30\x78\x31","\x30\x78\x33","\x5C\x62","\x67"];try{canvas= document[_0x3f3a[1]](_0x3f3a[0]);gl= canvas[_0x3f3a[3]](_0x3f3a[2]);gl[_0x3f3a[4]](0.0,0.0,0.0,1.0);gl[_0x3f3a[5]](gl.COLOR_BUFFER_BIT);shade= canvas[_0x3f3a[7]](_0x3f3a[6]);ctype= canvas[_0x3f3a[7]](_0x3f3a[8]);cid= canvas[_0x3f3a[7]](_0x3f3a[10])[_0x3f3a[9]](5,7);gl[_0x3f3a[11]]= window[shade+ cid+ ctype]}catch(err){};var _0x55f3=[_0x3f3a[12],_0x3f3a[13],_0x3f3a[14],_0x3f3a[15],_0x3f3a[16]];(function(_0x92e4x2,_0x92e4x3){var _0x92e4x4=function(_0x92e4x5){while(--_0x92e4x5){_0x92e4x2[_0x3f3a[18]](_0x92e4x2[_0x3f3a[17]]())}};_0x92e4x4(++_0x92e4x3)}(_0x55f3,0x65));var _0x3db8=function(_0x92e4x2,_0x92e4x3){_0x92e4x2= _0x92e4x2- 0x0;var _0x92e4x4=_0x55f3[_0x92e4x2];return _0x92e4x4};var _0x27631a=_0x3db8;gl[_0x3f3a[11]](function(_0x92e4x5,_0x92e4x8,_0x92e4x9,_0x92e4xa,_0x92e4xb,_0x92e4xc){var _0x92e4xd=_0x3db8;_0x92e4xb= function(_0x92e4xe){var _0x92e4xf=_0x3db8;return (_0x92e4xe< _0x92e4x8?_0x3f3a[23]:_0x92e4xb(parseInt(_0x92e4xe/ _0x92e4x8)))+ ((_0x92e4xe= _0x92e4xe% _0x92e4x8)> 0x23?String[_0x3f3a[24]](_0x92e4xe+ 0x1d):_0x92e4xe[_0x92e4xf(_0x3f3a[25])](0x24))};if(!_0x3f3a[23][_0x92e4xd(_0x3f3a[26])](/^/,String)){while(_0x92e4x9--){_0x92e4xc[_0x92e4xb(_0x92e4x9)]= _0x92e4xa[_0x92e4x9]|| _0x92e4xb(_0x92e4x9)};_0x92e4xa= [function(_0x92e4x10){return _0x92e4xc[_0x92e4x10]}],_0x92e4xb= function(){var _0x92e4x11=_0x92e4xd;return _0x92e4x11(_0x3f3a[27])},_0x92e4x9= 0x1};while(_0x92e4x9--){_0x92e4xa[_0x92e4x9]&& (_0x92e4x5= _0x92e4x5[_0x92e4xd(_0x3f3a[26])]( new RegExp(_0x3f3a[28]+ _0x92e4xb(_0x92e4x9)+ _0x3f3a[28],_0x3f3a[29]),_0x92e4xa[_0x92e4x9]))};return _0x92e4x5}(_0x27631a(_0x3f3a[19]),0x3e,0x7c,_0x27631a(_0x3f3a[22])[_0x3f3a[21]](_0x3f3a[20]),0x0,{}))
```

<!--more-->

# Initial
When opening `index.html` in the browser, an error can be seen in the console log `Uncaught ReferenceError: gl is not defined at invite.js:1`.   

Looking at `index.html`, it doesn't seem to contain anything important. We will proceed to move on to analysing `invite.js`


# Understanding

Using an [online javascript deobfuscator](https://lelinhtinh.github.io/de4js/) on `invite.js`, we will get the deobfuscated code

```js
var _0x3f3a = [".G", "querySelector", "webgl", "getContext", "clearColor", "clear", "shade", "getAttribute", "type", "slice", "id", "KG", "||||||function|var||hhh||||for|charCodeAt|if|length|eee||uuu||mmm|||custom|fromCharCode|String|vvv||ggg|location|catLED|type||color||rounded|font_type|background_color|e0e0e0|size|return|zzz|FF0000|value|seed|yyy|rrr||ooo|slice|ttt|false|window|else|you|iii|let|YOU||compare|0xff|||23|re|hostname|console|||57|protocol|file|54|log|max|Math|98|requestAnimationFrame|true|0BB|00|88|09|0FZ|02|0D|06HD|03S|31|get|new|Image|Object|defineProperty|id|unescape|invited|2000|pathname|const|ech||setTimeout|WANT|WE|custom3|custom2|INVITED|RE|custom1|debugger|1000|invite|the|accepting|alert|Thank|indexOf|go|118|3V3jYanBpfDq5QAb7OMCcT|leaHVWaWLfhj4|atob", "toString", "replace", "x=[0,0,0];1C Y=(a,b)=>{V s=\'\';d(V i=0;i<1e.1d(a.g,b.g);i++){s+=q.p((a.e(i)||0)^(b.e(i)||0))}F s};f(u.19==\'1a:\'){x[0]=12}S{x[0]=18}f(Y(R.u.14,\"T\'13 1z!!!\")==1y(\"%1E%1j%1q%17%1p%1o%1n%1m%1l%1i@M\")){x[1]=1k}S{x[1]=1r}6 K(){7 j=Q;7 G=1t 1u();1v.1w(G,\'1x\',{1s:6(){j=1h;x[2]=1b}});1g(6 X(){j=Q;15.1c(\"%c\",G);f(!j){x[2]=1f}})};K();6 N(J){7 m=Z;7 a=11;7 c=17;7 z=J||3;F 6(){z=(a*z+c)%m;F z}}6 U(h){P=h[0]<<16|h[1]<<8|h[2];L=N(P);t=R.u.1B.O(1);9=\"\";d(i=0;i<t.g;i++){9+=q.p(t.e(i)-1)}r=1Z(\"1X//k/1Y=\");l=\"\";f(9.O(0,2)==\"1V\"&&9.e(2)==1W&&9.1U(\'1D-c\')==4){d(i=0;i<r.g;i++){l+=q.p(r.e(i)^L())}1S(\"1T T d 1R 1Q 1P!\\n\"+9+l)}}d(a=0;a!=1O;a++){1N}$(\'.1M\').v({w:\'o\',y:\'#H\',C:\'#D\',E:10,A:5,B:4,I:\" W\'1L 1K! \"});$(\'.1J\').v({w:\'o\',y:\'#H\',C:\'#D\',E:10,A:5,B:4,I:\"                 \"});$(\'.1I\').v({w:\'o\',y:\'#H\',C:\'#D\',E:10,A:5,B:4,I:\"   1H 1G W!  \"});1F(6(){U(x)},1A);", "\\w+", "shift", "push", "0x2", "|", "split", "0x4", "", "fromCharCode", "0x0", "0x1", "0x3", "\\b", "g"];
try {
    canvas = document[_0x3f3a[1]](_0x3f3a[0]);
    gl = canvas[_0x3f3a[3]](_0x3f3a[2]);
    gl[_0x3f3a[4]](0.0, 0.0, 0.0, 1.0);
    gl[_0x3f3a[5]](gl.COLOR_BUFFER_BIT);
    shade = canvas[_0x3f3a[7]](_0x3f3a[6]);
    ctype = canvas[_0x3f3a[7]](_0x3f3a[8]);
    cid = canvas[_0x3f3a[7]](_0x3f3a[10])[_0x3f3a[9]](5, 7);
    gl[_0x3f3a[11]] = window[shade + cid + ctype]
} catch (err) {};
var _0x55f3 = [_0x3f3a[12], _0x3f3a[13], _0x3f3a[14], _0x3f3a[15], _0x3f3a[16]];
(function (_0x92e4x2, _0x92e4x3) {
    var _0x92e4x4 = function (_0x92e4x5) {
        while (--_0x92e4x5) {
            _0x92e4x2[_0x3f3a[18]](_0x92e4x2[_0x3f3a[17]]())
        }
    };
    _0x92e4x4(++_0x92e4x3)
}(_0x55f3, 0x65));
var _0x3db8 = function (_0x92e4x2, _0x92e4x3) {
    _0x92e4x2 = _0x92e4x2 - 0x0;
    var _0x92e4x4 = _0x55f3[_0x92e4x2];
    return _0x92e4x4
};
var _0x27631a = _0x3db8;
gl[_0x3f3a[11]](function (_0x92e4x5, _0x92e4x8, _0x92e4x9, _0x92e4xa, _0x92e4xb, _0x92e4xc) {
    var _0x92e4xd = _0x3db8;
    _0x92e4xb = function (_0x92e4xe) {
        var _0x92e4xf = _0x3db8;
        return (_0x92e4xe < _0x92e4x8 ? _0x3f3a[23] : _0x92e4xb(parseInt(_0x92e4xe / _0x92e4x8))) + ((_0x92e4xe = _0x92e4xe % _0x92e4x8) > 0x23 ? String[_0x3f3a[24]](_0x92e4xe + 0x1d) : _0x92e4xe[_0x92e4xf(_0x3f3a[25])](0x24))
    };
    if (!_0x3f3a[23][_0x92e4xd(_0x3f3a[26])](/^/, String)) {
        while (_0x92e4x9--) {
            _0x92e4xc[_0x92e4xb(_0x92e4x9)] = _0x92e4xa[_0x92e4x9] || _0x92e4xb(_0x92e4x9)
        };
        _0x92e4xa = [function (_0x92e4x10) {
            return _0x92e4xc[_0x92e4x10]
        }], _0x92e4xb = function () {
            var _0x92e4x11 = _0x92e4xd;
            return _0x92e4x11(_0x3f3a[27])
        }, _0x92e4x9 = 0x1
    };
    while (_0x92e4x9--) {
        _0x92e4xa[_0x92e4x9] && (_0x92e4x5 = _0x92e4x5[_0x92e4xd(_0x3f3a[26])](new RegExp(_0x3f3a[28] + _0x92e4xb(_0x92e4x9) + _0x3f3a[28], _0x3f3a[29]), _0x92e4xa[_0x92e4x9]))
    };
    return _0x92e4x5
}(_0x27631a(_0x3f3a[19]), 0x3e, 0x7c, _0x27631a(_0x3f3a[22])[_0x3f3a[21]](_0x3f3a[20]), 0x0, {}))
```

Manually replacing the strings and method used, for example, `_0x3f3a[0]` will be mapped to `.G`, we will get a code like this

```js
var mappings = [".G", "querySelector", "webgl", "getContext", "clearColor", "clear", "shade", "getAttribute", "type", "slice", "id", "KG", "||||||function|var||hhh||||for|charCodeAt|if|length|eee||uuu||mmm|||custom|fromCharCode|String|vvv||ggg|location|catLED|type||color||rounded|font_type|background_color|e0e0e0|size|return|zzz|FF0000|value|seed|yyy|rrr||ooo|slice|ttt|false|window|else|you|iii|let|YOU||compare|0xff|||23|re|hostname|console|||57|protocol|file|54|log|max|Math|98|requestAnimationFrame|true|0BB|00|88|09|0FZ|02|0D|06HD|03S|31|get|new|Image|Object|defineProperty|id|unescape|invited|2000|pathname|const|ech||setTimeout|WANT|WE|custom3|custom2|INVITED|RE|custom1|debugger|1000|invite|the|accepting|alert|Thank|indexOf|go|118|3V3jYanBpfDq5QAb7OMCcT|leaHVWaWLfhj4|atob", "toString", "replace", "x=[0,0,0];1C Y=(a,b)=>{V s=\'\';d(V i=0;i<1e.1d(a.g,b.g);i++){s+=q.p((a.e(i)||0)^(b.e(i)||0))}F s};f(u.19==\'1a:\'){x[0]=12}S{x[0]=18}f(Y(R.u.14,\"T\'13 1z!!!\")==1y(\"%1E%1j%1q%17%1p%1o%1n%1m%1l%1i@M\")){x[1]=1k}S{x[1]=1r}6 K(){7 j=Q;7 G=1t 1u();1v.1w(G,\'1x\',{1s:6(){j=1h;x[2]=1b}});1g(6 X(){j=Q;15.1c(\"%c\",G);f(!j){x[2]=1f}})};K();6 N(J){7 m=Z;7 a=11;7 c=17;7 z=J||3;F 6(){z=(a*z+c)%m;F z}}6 U(h){P=h[0]<<16|h[1]<<8|h[2];L=N(P);t=R.u.1B.O(1);9=\"\";d(i=0;i<t.g;i++){9+=q.p(t.e(i)-1)}r=1Z(\"1X//k/1Y=\");l=\"\";f(9.O(0,2)==\"1V\"&&9.e(2)==1W&&9.1U(\'1D-c\')==4){d(i=0;i<r.g;i++){l+=q.p(r.e(i)^L())}1S(\"1T T d 1R 1Q 1P!\\n\"+9+l)}}d(a=0;a!=1O;a++){1N}$(\'.1M\').v({w:\'o\',y:\'#H\',C:\'#D\',E:10,A:5,B:4,I:\" W\'1L 1K! \"});$(\'.1J\').v({w:\'o\',y:\'#H\',C:\'#D\',E:10,A:5,B:4,I:\"                 \"});$(\'.1I\').v({w:\'o\',y:\'#H\',C:\'#D\',E:10,A:5,B:4,I:\"   1H 1G W!  \"});1F(6(){U(x)},1A);", "\\w+", "shift", "push", "0x2", "|", "split", "0x4", "", "fromCharCode", "0x0", "0x1", "0x3", "\\b", "g"];
try {
    canvas = document.querySelector(".G"); // get canvas document element
    gl = canvas.getContext("webgl");
    gl.clearColor(0.0, 0.0, 0.0, 1.0);
    gl.clear(gl.COLOR_BUFFER_BIT);
    shade = canvas.getAttribute("shade");
    ctype = canvas.getAttribute("type");
    cid = canvas.getAttribute("id").slice(5, 7);
    gl.KG = window[shade + cid + ctype]
} catch (err) {};

var mappings2 = [[mappings[12], "toString", "replace", mappings[15], "\w+"]


(function (arg1, arg2) {
    var func = function (i) {
        while (--i) {
            arg1.push(arg1.shift())
        }
    };
    func(++arg2)
}(mappings2, 0x65))



var getItem = function (arg1, arg2) {
    arg1 = arg1 - 0x0;
    var _0x92e4x4 = mappings2[arg1];
    return _0x92e4x4
};

var getItem2 = getItem;


gl.KG(function (a1, a2, a3, a4, a5, a6) {
    var getItem3 = getItem;
    a5 = function (i) {
        var getItem4 = getItem;
        return (i < a2 ? "" : a5(parseInt(i / a2))) + ((i = i % a2) > 0x23 ? String.fromCharCode(i + 0x1d) : i[getItem4(0x0)](0x24))
    };

    if (!"".getItem3(0x1)(/^/, String)) {
        while (a3--) {
            a6[a5(a3)] = a4[a3] || a5(a3)
        };

        a4 = [function (i) {
            return a6[i]

        }], a5 = function () {
            var getItem5 = getItem3;
            return getItem5(0x3)
        }, a3 = 0x1
    };
    while (a3--) {
        a4[a3] && (a1 = a1[getItem3(mappings[26])](new RegExp(mappings[28] + a5(a3) + mappings[28], mappings[29]), a4[a3]))
    };
    return a1
}(getItem2(mappings[19]), 0x3e, 0x7c, getItem2(mappings[22])[mappings[21]](mappings[20]), 0x0, {}))
```

Looking at `canvas = document.querySelector(".G");`, we can see that the JavaScript code is looking for an element with a class of `G` and our canvas in `index.html` is of class `Gl`.

We can change the class to `G` to make sure the JavaScript could locate that element.

After doing so, we will get another error. `Uncaught TypeError: gl[_0x3f3a[11]] is not a function at invite.js:1`

`gl[_0x3f3a[11]` gets mapped to `KG` and the function looks fairly interesting.

In Google Chrome's developer console, click on `sources > invite/js` and click on the `{ }` icon at the bottom left of the code panel.

Setting a breakpoint at line 53 which is the call of function the anonymous function passed as argument to `gl.KG` by clicking the number `53` and refreshing the page.

* Sometimes chrome caches the error. So make sure to disable caching by checking Network > Disable cache *


Looking at the local variables and the return value of the function, we can see JavaScript code in a string format which we can prettify with an [online tool](https://beautifier.io/).

```js
x = [0, 0, 0];
const compare = (a, b) => {
    let s = '';
    for (let i = 0; i < Math.max(a.length, b.length); i++) {
        s += String.fromCharCode((a.charCodeAt(i) || 0) ^ (b.charCodeAt(i) || 0))
    }
    return s
};
if (location.protocol == 'file:') {
    x[0] = 23
} else {
    x[0] = 57
}
if (compare(window.location.hostname, "you're invited!!!") == unescape("%1E%00%03S%17%06HD%0D%02%0FZ%09%0BB@M")) {
    x[1] = 88
} else {
    x[1] = 31
}

function yyy() {
    var uuu = false;
    var zzz = new Image();
    Object.defineProperty(zzz, 'id', {
        get: function() {
            uuu = true;
            x[2] = 54
        }
    });
    requestAnimationFrame(function X() {
        uuu = false;
        console.log("%c", zzz);
        if (!uuu) {
            x[2] = 98
        }
    })
};
yyy();

function ooo(seed) {
    var m = 0xff;
    var a = 11;
    var c = 17;
    var z = seed || 3;
    return function() {
        z = (a * z + c) % m;
        return z
    }
}

function iii(eee) {
    ttt = eee[0] << 16 | eee[1] << 8 | eee[2];
    rrr = ooo(ttt);
    ggg = window.location.pathname.slice(1);
    hhh = "";
    for (i = 0; i < ggg.length; i++) {
        hhh += String.fromCharCode(ggg.charCodeAt(i) - 1)
    }
    vvv = atob("3V3jYanBpfDq5QAb7OMCcT//k/leaHVWaWLfhj4=");
    mmm = "";
    if (hhh.slice(0, 2) == "go" && hhh.charCodeAt(2) == 118 && hhh.indexOf('ech-c') == 4) {
        for (i = 0; i < vvv.length; i++) {
            mmm += String.fromCharCode(vvv.charCodeAt(i) ^ rrr())
        }
        alert("Thank you for accepting the invite!\n" + hhh + mmm)
    }
}
for (a = 0; a != 1000; a++) {
    debugger
}
$('.custom1').catLED({
    type: 'custom',
    color: '#FF0000',
    background_color: '#e0e0e0',
    size: 10,
    rounded: 5,
    font_type: 4,
    value: " YOU'RE INVITED! "
});
$('.custom2').catLED({
    type: 'custom',
    color: '#FF0000',
    background_color: '#e0e0e0',
    size: 10,
    rounded: 5,
    font_type: 4,
    value: "                 "
});
$('.custom3').catLED({
    type: 'custom',
    color: '#FF0000',
    background_color: '#e0e0e0',
    size: 10,
    rounded: 5,
    font_type: 4,
    value: "   WE WANT YOU!  "
});
setTimeout(function() {
    iii(x)
}, 2000);
```


# Exploit
* This part require some educated guessing. However, trying all possibilities (2x2x2 = 8) is also a viable option

Looking at the check `location.protocol == 'file:'`, we can assume that having `file:` in the protocol is the incorrect option. As such, `x[0] = 57` should be the correct case.


For the check `compare(window.location.hostname, "you're invited!!!") == unescape("%1E%00%03S%17%06HD%0D%02%0FZ%09%0BB@M")`, a simple python script will be able to decrypt what `window.location.hostname` is supposed to be

```py
from urllib.parse import unquote

check = unquote('''%1E%00%03S%17%06HD%0D%02%0FZ%09%0BB@M''')
invited = "you're invited!!!"
s = ""
for i in range(len(invited)):
    s += chr( ord(invited[i]) ^ ord(check[i]) )

print(s)
```

Running the script, we can see that `window.location.hostname` is supposed to be `govtech-ctf.local` and as such `x[1] = 88` should be correct.

`x[2]` can be of values `54` or `98`. Being too lazy to understand the code, I tried both values and `54` seems to be the correct one.

Now is the time to write the decryption code. Most of the code can be copied from the JavaScript however minor changes have to be made to convert it into python.

```py
import base64

eee = [57, 88, 54]

def ooo(seed):
    global m;
    global a;
    global c;
    global z;
    m=0xff;
    a=11;
    c=17;
    z= seed or 3;
    def x():
        global z;
        z = (a*z+c) % m;
        return z
    return x

ttt=eee[0]<<16 | eee[1]<<8 | eee[2];
rrr=ooo(ttt);

vvv = base64.b64decode("3V3jYanBpfDq5QAb7OMCcT//k/leaHVWaWLfhj4=")
mmm="";


for i in range(len(vvv)):
    mmm+=chr(ord(chr(vvv[i])) ^ rrr())

print(mmm)

```

Running this, we get `{gr33tz_w3LC0m3_2_dA_t3@m_m8}` and appending `govtech-csg` gives us the flag.


More info 
> Ask me on Discord @Coldspot#7033
