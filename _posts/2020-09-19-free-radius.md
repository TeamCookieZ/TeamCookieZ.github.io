---
title: Free Radius 
author: Lim Kai Xian (AxiaMil)
date: 2020-09-24 00:34:00 +0800
categories: [Blogging, Tutorial]
tags: [autentication, tech, open-source]
toc: false
---


[Remote Authentication Dial-In User Service](https://en.wikipedia.org/wiki/RADIUS) also known as **`RADIUS`** is a client-server networking protocol 
used for authentication in a network. It comprises of two component for it to work which is a client and a server. The client is the device you as an
administrators wants people to authenticate while the server would serve this authenitcation request by checking the credentials with it's database.

Usually the RADIUS client is a NAS while the RADIUS server is a WIndows NT or UNIX machine.

It can be used in both Unix and Windows system to ensure AAA (Authentication, Authorization & Accounting).

It can be used in a home network (NAS) to ensure authentication when accessing the NAS.
![upload-image](/assets/img/sample/RADIUS-Server.gif)

## How does it work?
1. User sends a form of authentication to the RADIUS Client
2. Client prompts for credentials 
3. User replies with the credentials
4. RADIUS client forwards the encrypted credentials to the RADIUS server
5. RADIUS server replies with a reply of either `Accept`, `Reject`, or `Challenge`
6. RADIUS client then based on the result of the server reply, it performs it's action

## RADIUS vs TACACS+

`RADIUS` is **open source** and can be used anywhere while `TACACS+` is **CISCO proprietary**.
However, TACACS+ is more secure and reliable as it uses TCP and it fully encrypts packets.

## How to get started

A quick, popular and easy way is with [**FreeRADIUS**](https://freeradius.org/).

#### Alternatives to freeRADIUS
- Devise
- Auth0
- 0Auth2
- LoginRadius

#### Setup
**NOTE (Debian based devices would be called freeradius instead of radiusd hence switch the commands from freeradius to radiusd if it does not work)**

1. Install the server
```
$sudo apt install freeradius
```

Debian-based systems

2. Startup the freeradius server(as root)
```
$sudo freeradius -X 
```

**NOTE (When there is an error when running the startup)**
>> the error is usually due to a current radius already running, hence we would need to kill it to run the current freeradius 
```
$sudo lsof -i:[port]
$sudo killall freeradius
$sudo free radius -X
```

3. Testing of freeradius

To test the freeradius, we can use the radtest commands

firstly, edit the `raddb/mods-config/file/authorize` and add the following line of text at the top of the file, before anything else
```
testing Cleartext-Password := "password"
```
![upload-image](/assets/img/sample/added-testing-code.png)
```
$radtest testing password 127.0.0.1 0 testing123
```
![upload-image](/assets/img/sample/radtest-testing-successful.png)


4. Adding clients
To add a client edit the `clients.conf` file by adding the following content
```
client new {
	ipaddr = 192.0.2.1
	secret = testing123
	shortname = testing
}
```
>> change the ip address to the client ip address and the secret to the password that you want to use
>> use ipv6addr for IPv6 Address instead of ipaddr
>> 

More info 
>> Main configuration file is called radiusd.conf in the root folder of the freeradius file 
>> Listening, Proxy, Authentication configuration are in the sites-available/default file