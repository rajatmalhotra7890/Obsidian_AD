# The forest has trust issues

- Now that we have dumped credentials on the domain controller, we can utilize these credentials to find other domains and forests that we can gain a foothold on.
- We can begin by using offensive powershell or bloodhound to find a forest trust, then use credentials to access a segmented domain controller.

## Domain Trusts Overview

- Trusts are a mechanism in place for users in the network to gain access to other resources in the domain. For the most part, trusts outline the way that the domains inside of a forest communicate to each other, in some environments trusts can be extended out to external domains and even forests in some cases.


## Hunting for an Attack Surface
- We can utilize either offensive powershell or bloodhound, both give the same amount of information however they give different ways of presenting the data. Utilize powerview or bloodhound to enumerate the trusts within the network.


From BloodHound results, we see that there is a trust between `THROWBACK.local` and `CORPORATE.local`.


## Using chisel to setup proxies
[Multiple Chisel pivots](obsidian://open?vault=THM%20Networks&file=Knowledge%20Base%2FPivoting%20Techniques%2F3.%20Chisel)


### Make or break pivoting Tip (Really crucial)
- After deploying a second pivot and getting a connect on a different port, comment out the first proxy configuration running from proxychains.conf

![[Pasted image 20221027005214.png]]
- Let the first proxy run but in order to use the second pivot proxy, before actually using it, comment out the first one.

Tip #2  - Read the above blog thoroughly in order to understand multiple proxy usage of chisel. It's really crucial!


## Questions

1. What domain has a trust relationship with THROWBACK.local?
`CORPORATE.local`

2. What is the hostname of the machine that has a forest trust with the domain controller?
`CORP-DC01`

3. What is the Administrator account we can use to access the second forest?
`mercerh`

4. What is the name of the file in the Administrator's Documents folder?
`server_update.txt`

## Important Note for enumeration
- When you get a set of sensitve credentials on a domain controller such as the type of mercerh, always RDP and check `Server Manager` on the Domain Controller to observe contents of `Active Directory Domain and Trusts`
- Then use the domain admin credentials on the trusted domain too! You never know!


`server_update.txt` contents
```
Hey team! Happy Thursday!

Not much on the schedule for this week, we are continuing our transition to our new
servers please be patient with us as we make this transition.

In order to access your usual resources please go to mail.corporate.local where you will
find our new emailing service, as well as breachgtfo.local where you will find our
proprierty breach service that all of you are already used to.
If you have not already please add 10.200.x.232 to your hosts file in order to access these resources.

As we are auditing our infrastructure please remeber that no personal social media
accounts should be connected to company resources such as github. If you need to use twitter to make company announcments
please use the @tbhSecurity twitter.

Please remain patient during this transition and dont be afraid to email me or any of the
other team members with questions

Summers Winters,
CEO of Throwback Hacks Security
```


Flag from twitter - `TBH{ca57861454b195f6a5c951a634e05f9e}`
Root Flag on CORP-DC01 (10.200.34.118) -  `TBH{d2368a76214103ac670a7984b4dba5a3}`
User Flag on CORP-DC01 - `TBH{773e16d57284363e68a4db254860aed1

Since MercerH is also an administrator on CORP-DC01, we can access every resource and hence all the user and root flags.




### Since we have shell on CORP-DC01, we must set up another proxy server on this domain controller machine!
- Then use crackmapexec to discover new machines

Two new machines we discover are:
```
SMB         10.200.34.243   445    CORP-ADT01       [*] Windows 10.0 Build 19041 x64 (name:CORP-ADT01) (domain:corporate.local) (signing:False) (SMBv1:False)

SMB         10.200.34.79    445    TBSEC-DC01       [*] Windows 10.0 Build 17763 x64 (name:TBSEC-DC01) (domain:TBSECURITY.local) (signing:True) (SMBv1:False)
```

Also check Nmap scan results! I've updated it there as well!