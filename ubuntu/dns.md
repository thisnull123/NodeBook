

# Install and configure DNS server in Ubuntu 16.04 LTS

Primary DNS server:

+ Operating system : Ubuntu 16.04 LTS 64 bit server
+ Hostname : pri.ostechnix.lan
+ IP address : 192.168.1.200/24

Secondary DNS server:

+ Operating system : Ubuntu 16.04 LTS 64 bit server
+ Hostname : sec.ostechnix.lan
+ IP address : 192.168.1.201/24

DNS Client:

+ Operating system : Ubuntu 16.04 LTS 64 bit server
+ Hostname : client.ostechnix.lan
+ IP address : 192.168.1.202/24

## Install and Configure DNS server in Ubuntu 16.04

I will split this guide as as three parts for the sake of simplicity and easy understanding.

1. Install and configure Caching-only name server,
2. Install and configure Primary DNS server or Master DNS server
3. Install and configure Secondary DNS server or Slave DNS server

### Install and configure Caching-only name server

run one of below

```shell
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

Install BIND9

After updating the system, run the following command to install BIND9 packages which are used to setup DNS server.

```shell
sudo apt-get -y install bind9 bind9utils bind9-doc
```


Configuring Caching name server

Caching name server saves the DNS query results locally for a particular period of time. It reduces the DNS server’s traffic by saving the queries locally, therefore it improves the performance and efficiency of the DNS server.

To configure Caching name server, edit `/etc/bind/named.conf.options` file:

`sudo nano /etc/bind/named.conf.options`

Uncomment the following lines. And then, add your ISP or Google public DNS server IP addresses.

```
forwarders {
 8.8.8.8;
 };
```

restart bind9 service to take effect the changes.

```
sudo systemctl restart bind9
```

>Testing Caching name server
Now let us check if it is working or not using command:
```
dig -x 127.0.0.1
```

## Install and configure Primary DNS server


```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade

sudo apt-get install bind9 bind9utils bind9-doc
```

Configuring Primary DNS server

All configuration file be will be available under `/etc/bind/` directory.

Let us edit bind9 configuration file

Edit ‘/etc/bind/named.conf’ using any editor of your choice:

    sudo nano /etc/bind/named.conf

This file should have the following lines in it. If the lines are not there, just add them.

```
include "/etc/bind/named.conf.options";
include "/etc/bind/named.conf.local";
include "/etc/bind/named.conf.default-zones";
```

https://www.ostechnix.com/install-and-configure-dns-server-ubuntu-16-04-lts/