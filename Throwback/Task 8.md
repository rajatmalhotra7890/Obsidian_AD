# Exploring the Caverns
- You and your team have run your scans and it is now time to visit the web servers and see what services are running on them. Your team decides that it is best to enumerate THROWBACK-PROD, THROWBACK-MAIL, then THROWBACK-FW01.

## Enumerating Web Servers -
It is important to enumerate what is running on a web server further than just a scan. To get an understanding of what services are on the network and what could possibly be used as an attack vector.

## Enumerating THROWBACK-PROD's Production Server -
- Upon initial access to the production server, we can see that it is a company website advertising themselves as a private penetration testing and analysis firm.

![[Pasted image 20220925095814.png]]
- Further inspection of the website reveals a list of employees, location of the company, and an email address. These details can be important to note for later attacks and enumeration. 

## Enumerating THROWBACK-MAIL's Mail Server -
- When enumerating the THROWBACK-MAIL web server we find from the source code that it is running squirrel mail as a mail service for the company.

![[Pasted image 20220925095905.png]]
- When viewing the banner we find that there is a guest login account that anyone can use. We will need these credentials for later attacks.


## Enumerating THROWBACK-FW01's Service -
- Immediately upon visiting THROWBACK-FW01 we can tell that it is running a new version of pfSense. As this firewall is accessible to the public we can assume that is is an outside firewall designed to keep attackers out.

![[Pasted image 20220925095956.png]]
- Your team informs you that it is your decision of what target to attack first, all can be good attack paths. They suggest attacking THROWBACK-FW01 first however the decision is yours.



### Observations
1. Use wappalyzer and see the services running on all the servers hosting a web server on port 80 or 8080 or 143.
2. Now we see that on Mail server, we have a web server and we have guest credentials posted right on the web page of Throwback-Mail
3. Check Page Source, bust some hidden dirs and see if anything comes up.

- Check around after guest login and here we see all the emails come up of different domain users.
![[Pasted image 20220925100716.png]]


## Questions

1. Who is the CEO of Throwback Hacks?  
`Summer Winters`

2. Where is the company located?
`Great Britain`

3. What is the guest username on the mail server?
`tbhguest`

4. What is the guest password on the mail server?
`WelcomeTBH1!`


