---
title: DNS Server using Bind9
author: Lim Kai Xian (AxiaMil)
date: 2020-09-30 21:39:00 +0800
categories: [Networking]
tags: [tech, open-source, networking]
toc: false
---

A [domain Name System (DNS)](https://en.wikipedia.org/wiki/Domain_Name_System) server converts a domain name into an ip address. 
[Berkeley Internet Name Domain (BIND)](https://en.wikipedia.org/wiki/BIND) is the most popular software of the implementation of DNS
server. It was developed in the 1980s at the University of Berkley. 

Bind9 is the version 9 of the open source BIND version.

### 1. Installing Bind9 
[CentOS 7]
```
$yum install bind bind-utils
```

[Ubuntu]
```
$apt install bind9 bind9utils bind9-doc dnsutils
```

### 2. Configuring the DNS (You Might Need to Swtich to root)
[CentOS 7]
```
$nano /etc/named.conf
```

Edit the named.conf to:
##### 2.1 Configure DNS to listen to an IP address
[CentOS 7]
```
listen-on port 53 { 127.0.0.1; 192.168.42.134 }
```
Change the 192.168.42.134 to the ip-address you want to listen to

##### 2.2 Configure DNS to allow query from
[CentOS 7]
```
allow-query { localhost; 192.168.42.0/24; }
```
Change the network 192.168.42.0/24 to your network or a specific IP address 
![upload-image](/assets/img/sample/free-radius/named-conf-configuration.png)

[Ubuntu]
```
$cd /etc/bind/
$nano named.conf.options
```
Add the line into the file
##### 2.1 Configure DNS to listen to an IP address
```
listen-on port 53 { 127.0.0.1; 192.168.42.134 }
```
Change the 192.168.42.134 to the ip-address you want to listen to

##### 2.2 Configure DNS to allow query from
[Ubuntu]
```
allow-query { localhost; 192.168.42.0/24; }
```
Change the network 192.168.42.0/24 to your network or a specific IP address 

### 3. Zones
There are two different types of zones, they are master or slave. A slave gets their zone information through a zone transfer from another DNS server
while a master gets their zone information from admin configuration or other means and it is able to operate without the need of other DNS server

The sample folders for these files are located in the /usr/share/doc/bind/sample/

For CentOS 7 Continuing to edit the `/etc/named.conf`, to:

While, to add configurations for local zones in Ubuntu add it in `/etc/bind/named.conf.local`,
Add other zones by creating a new file with the `.conf` file format and include the file in the `named.conf` file

##### 3.1 Forward Zones
Converts Domain name to IP address

[Master Zone]
Add the following code 
```
zone "test.axiamil.me" IN {
	type master;
	file "/var/bind/forward.test.axiamil.me.db";
	allow-update { none; };

}
```
>> Change test.axiamil.me to your domain name
>> Change "/var/bind/forward.test.axiamil.me.db" to your forward lookup file
>> Change "/var/bind/" to "/var/named/" if using CentOS 7

[Slave Zone]
Add the following code
```
zone "google.com" {
	type slave;
	masters { 198.51.100.1; 220.20.3.2; };
	file "/var/bind/forward.google.com.db";
}
>> Change google.com to the domain name
>> Change 198.51.100.1 and 220.20.3.2 to the other DNS server you want to refer to
>> Change "/var/bind/" to "/var/named/" if using CentOS 7

```
##### 3.2 Reverse Zones
To fully understand reverse zone, 
[click here [blog]](https://www.sciencedirect.com/topics/computer-science/reverse-lookup-zone)
[click here (video)](https://www.youtube.com/watch?v=7KN-_IWs7hk)

In summary, reverse zone also known as reverse lookup zone basically converts the ip address to a domain name.
Like its name, the ip address is also reversed and the network of 192.168.42.0/24 would be converted into 42.168.192.in-addr.arpa

[Master]
Add the following code
```
zone "42.168.192.in-addr.arpa" IN {
	type master;
	file "/var/bind/reverse.test.axiamil.me.db";
	allow-update { none; };
}
```
>> Change 42.168.192.in-addr.arpa to your reverse lookup name
>> Change "/var/bind/reverse.test.axiamil.me.db" to your reverse lookup file
>> Change "/var/bind/" to "/var/named/" if using CentOS 7

[Slave]
Add the following code 
```
zone "125.200.138.in-addr.arpa" IN {
	type slave;
	masters { 198.51.100.1; 220.20.3.2; };
	file "/var/bind/reverse.google.axiamil.me.db";
}
```
>> Change 198.51.100.1 and 220.20.3.2 to the other DNS server you want to refer to
>> Change "/var/bind/reverse.google.axiamil.me.db" to your reverse lookup file
>> Change "/var/bind/" to "/var/named/" if using CentOS 7

##### 3.3 Zone Files
Add all zone files into the /etc/bind/ files
```
$cd /etc/bind/
$cp db.empty forward.test.axiamil.me.db
$nano forward.test.axiamil.db
```

Edit the configuration to get the DNS record you want, 

For example:
To add an A record 
```
@	IN	A	127.0.0.1
www IN  A   192.168.3.2
```

To add an Pointer record 
```
1.0.0	IN	PTR	localhost.
```

To add a Name Server (NS) record
```
ns1 IN  A       192.168.0.10
```

To add a CNAME record
```
ftp     IN CNAME        www.cool.com
```

To add a Mail Exchange (MX) record 
```
cool.com. IN  MX 10   mail.cool.com.
```

##### 3.4 Adding the Results
Go to a Client Machine and add the DNS server IP address in the `/etc/resolv.conf`
```
$nameserver 192.168.42.131
```

>> Change the IP address to your nameserver IP address

Save and Close the file 
[Ubuntu]
```
$systemctl restart bind9
```

[CentOS 7]
```
systemctl restart NetworkManager
```


>> Change the IP address to the IP address that you configured
##### 3.5 Testing out the DNS
Check for any syntax error by
```
$named-checkzone forward.example forward.example.com
```

If there is no error there would be an `'OK'` shown

Verifying if the forward lookup work
```
$dig www.cool.com
$dig test.axiamil.me
```
>> Change the domain name to your domain name that you configured

Verifying reverse Lookuo
```
$dig -x 192.168.32.12
```


More Info 
>> You can also try Chrooting BIND9 for security so that it has access to the resources it needs only
>> For new Ubuntu releases, AppArmour is installed by default so there would not be need for chrooting BIND9 unless the AppArmour is disabled explicitly.

Similar Blog Posts : 
>> [Median (Ubuntu](https://medium.com/@Alibaba_Cloud/how-to-setup-dns-server-using-bind9-on-ubuntu-16-04-cf3ce7f570ec)
>> [itzgeek [CentOS 7]](https://www.itzgeek.com/how-tos/linux/centos-how-tos/configure-dns-bind-server-on-centos-7-rhel-7.html)
>> [Wiki [Bind9]](https://wiki.debian.org/Bind9)
>> [Bind9 Howto [Ubuntu Forum]](https://help.ubuntu.com/community/BIND9ServerHowto)