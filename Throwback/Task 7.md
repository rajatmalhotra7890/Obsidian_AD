# Entering the Breach
- Your attack team runs initial recon on the target `Throwback Hacks Security`
	- They find there are 3 machines that are public facing:
		1. `THROWBACK-PROD`
		2. `THROWBACK-FW01`
		3. `THROWBACK-MAIL`

- Your team has informed that these assets are publicly facing, so its your job to perform additional recon on these machines and find a way in.

So, we will be using the tool Nmap


`Scanning the World with nmap`

- nmap is a commonly used port scanning tool that is an industry standard that is both fast and comes with NSE scripts. nmap also supports CIDR notation so we can specify a /24 to specify 254 hosts.

We can specify how we want to scan the hosts using switches.

    sV determines service and version of open ports

    sC runs a script scan against the found ports

    -p- scans all ports 0-65535

    -v runs the scan in verbose mode


Hosts responding to scans
```
10.200.53.219 - THROWBACK.PROD 
10.200.53.138 - THROWBACK-FW01
10.200.53.232 - THROWBACK.MAIL
```

Nmap Results are as follows 

PROD - `10.200.53.219`
```nmap
Nmap scan report for 10.200.53.219
Host is up (0.32s latency).
Not shown: 65524 filtered tcp ports (no-response)
PORT      STATE SERVICE       VERSION
22/tcp    open  ssh           OpenSSH for_Windows_7.7 (protocol 2.0)
| ssh-hostkey: 
|   2048 85:b8:1f:80:46:3d:91:0f:8c:f2:f2:3f:5c:87:67:72 (RSA)
|   256 5c:0d:46:e9:42:d4:4d:a0:36:d6:19:e5:f3:ce:49:06 (ECDSA)
|_  256 e2:2a:cb:39:85:0f:73:06:a9:23:9d:bf:be:f7:50:0c (ED25519)

80/tcp    open  http          Microsoft IIS httpd 10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-title: Throwback Hacks
|_http-server-header: Microsoft-IIS/10.0

135/tcp   open  msrpc         Microsoft Windows RPC

139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn

445/tcp   open  microsoft-ds?

3389/tcp  open  ms-wbt-server Microsoft Terminal Services
|_ssl-date: 2022-09-25T02:29:41+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=THROWBACK-PROD.THROWBACK.local
| Issuer: commonName=THROWBACK-PROD.THROWBACK.local
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2022-09-24T01:03:23
| Not valid after:  2023-03-26T01:03:23
| MD5:   9f8f c353 7d3f 05db 05f6 f677 2720 13ce
|_SHA-1: 0eed 3b87 dca0 c306 5862 cff9 618a 2e45 f7b1 1200
| rdp-ntlm-info: 
|   Target_Name: THROWBACK
|   NetBIOS_Domain_Name: THROWBACK
|   NetBIOS_Computer_Name: THROWBACK-PROD
|   DNS_Domain_Name: THROWBACK.local
|   DNS_Computer_Name: THROWBACK-PROD.THROWBACK.local
|   DNS_Tree_Name: THROWBACK.local
|   Product_Version: 10.0.17763
|_  System_Time: 2022-09-25T02:29:01+00:00

5357/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Service Unavailable

5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49667/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49673/tcp open  msrpc         Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2022-09-25T02:29:06
|_  start_date: N/A
```

MAIL - `10.200.53.232`
```nmap
Nmap scan report for 10.200.53.232
Host is up (0.18s latency).
Not shown: 65531 closed tcp ports (reset)
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 a7:5c:ea:06:5f:7d:76:47:f5:1a:bb:2e:bc:57:0f:27 (RSA)
|   256 5f:83:b8:c6:b7:4e:8d:26:9d:0b:71:41:fe:af:46:23 (ECDSA)
|_  256 e6:5b:7d:dd:96:94:c8:0f:89:5d:d7:df:2d:f5:69:5b (ED25519)

80/tcp  open  http     Apache httpd 2.4.29 ((Ubuntu))
| http-title: Throwback Hacks - Login
|_Requested resource was src/login.php
|_http-favicon: Unknown favicon MD5: 2D267521ED544C817FADA219E66C0CCC
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.29 (Ubuntu)

143/tcp open  imap     Dovecot imapd (Ubuntu)
|_imap-capabilities: more IDLE have post-login IMAP4rev1 STARTTLS ID capabilities Pre-login OK ENABLE LOGINDISABLEDA0001 SASL-IR listed LOGIN-REFERRALS LITERAL+
| ssl-cert: Subject: commonName=ip-10-40-119-232.eu-west-1.compute.internal
| Subject Alternative Name: DNS:ip-10-40-119-232.eu-west-1.compute.internal
| Issuer: commonName=ip-10-40-119-232.eu-west-1.compute.internal
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2020-07-25T15:51:57
| Not valid after:  2030-07-23T15:51:57
| MD5:   adc4 c6e2 d74f d9eb ccde 96aa 5780 bb69
|_SHA-1: 93aa 5da0 3829 8ca3 aa6b f148 4f92 1ed0 c568 a942
|_ssl-date: TLS randomness does not represent time

993/tcp open  ssl/imap Dovecot imapd (Ubuntu)
|_imap-capabilities: IDLE have more IMAP4rev1 post-login ID LOGIN-REFERRALS Pre-login OK ENABLE capabilities SASL-IR listed AUTH=PLAINA0001 LITERAL+
| ssl-cert: Subject: commonName=ip-10-40-119-232.eu-west-1.compute.internal
| Subject Alternative Name: DNS:ip-10-40-119-232.eu-west-1.compute.internal
| Issuer: commonName=ip-10-40-119-232.eu-west-1.compute.internal
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2020-07-25T15:51:57
| Not valid after:  2030-07-23T15:51:57
| MD5:   adc4 c6e2 d74f d9eb ccde 96aa 5780 bb69
|_SHA-1: 93aa 5da0 3829 8ca3 aa6b f148 4f92 1ed0 c568 a942
|_ssl-date: TLS randomness does not represent time
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

FW01 - `10.200.53.138`
```nmap
Nmap scan report for 10.200.53.138
Host is up (0.17s latency).
Not shown: 65531 filtered tcp ports (no-response)
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 7.5 (protocol 2.0)
| ssh-hostkey: 
|_  4096 38:04:a0:a1:d0:e6:ab:d9:7d:c0:da:f3:66:bf:77:15 (RSA)

53/tcp  open  domain   (generic dns response: REFUSED)

80/tcp  open  http     nginx
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Did not follow redirect to https://10.200.53.138/

443/tcp open  ssl/http nginx
| ssl-cert: Subject: commonName=pfSense-5f099cf870c18/organizationName=pfSense webConfigurator Self-Signed Certificate
| Subject Alternative Name: DNS:pfSense-5f099cf870c18
| Issuer: commonName=pfSense-5f099cf870c18/organizationName=pfSense webConfigurator Self-Signed Certificate
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2020-07-11T11:05:28
| Not valid after:  2021-08-13T11:05:28
| MD5:   fe06 fa47 4d83 8454 e67a 1840 7ea8 d101
|_SHA-1: 672e 5f8f 9b28 7cad 5789 c5be cb1c f3f2 6c63 dfb2
|_http-title: pfSense - Login
| http-methods: 
|_  Supported Methods: GET HEAD POST
|_http-favicon: Unknown favicon MD5: 5567E9CE23E5549E0FCD7195F3882816
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port53-TCP:V=7.92%I=7%D=9/24%Time=632FC9A1%P=x86_64-pc-linux-gnu%r(DNSV
SF:ersionBindReqTCP,E,"\0\x0c\0\x06\x81\x05\0\0\0\0\0\0\0\0");

```

`10.200.53.250`
```nmap
Nmap scan report for 10.200.53.250
Host is up (0.17s latency).
Not shown: 65533 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 5e:3c:9b:ac:a3:be:be:be:56:15:a5:dd:e7:78:63:87 (RSA)
|   256 5f:77:af:9d:d3:ee:1b:81:c2:87:e7:54:af:b6:ff:05 (ECDSA)
|_  256 28:71:b5:62:50:b6:2e:3e:b6:30:b6:1f:65:b4:be:db (ED25519)

1337/tcp open  http    Node.js Express framework
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Error
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```

## Questions

1. What is the domain name? 
`THROWBACK.local`

2. What is the HTTP title of the web server running on THROWBACK-PROD?
`Throwback Hacks`

3. How many ports are open on THROWBACK-MAIL?
`4`

4. What service is running on THROWBACK-FW01?
`pfSense firewall`

5. What version of Apache is running on THROWBACK-MAIL?
`Apache/2.4.29`



More info on Port 143 - [143 Port TCP](https://monsterhost.com/what-everyone-must-know-about-imap-port/) - IMAP whereas Port 993 is simply IMAP over SSL.


