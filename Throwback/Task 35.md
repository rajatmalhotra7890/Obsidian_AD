# Lost and Found

- Now we have a list of emails from Linkedin, we can format them into a custom wordlist with email format we got from CORP-ADT01 and put them into a breached credentials service like HaveIBeenPwned or Dehashed to see if any breaches compromised victim email.

In our case we will use an internal breached credentials server 



## Introduction to Data Breaches
At the time of writing, HaveIBeenPwned has a collection of 10,189,054,980 breached user accounts, as well as 473 total breached websites. This is an alarmingly high number, but can offer a lot to an attacker looking to get an easy win. Data Breaches can confirm many things, not just if a user has been hacked, but it also confirms than an email account exists. This is arguably more valuable than a password. You can use this information in combination with Phishing to gain some really easy wins within an organization. For this next exercise, we have setup a Breach Credential Lookup service called Breach || GTFO, a fake service within the network that is modeled after [https://dehashed.com](https://dehashed.com/) -- A paid breach credential lookup service.


- Now we need to generate a wordlist of emails which would match the new format of emails in Throwback Corp Email Server.

## Hence we use a tool called `Namely` which will build us a domain user wordlist 
- Basically it takes a name or multiple domain names and generates a wordlist around the two.
- Namely can also take custom template keys in order to customize the wordlist to your needs.

# Step1 - Installing Namely

1.) `cd /opt`

2.) `sudo git clone https://github.com/OrielOrielOriel/namely`


# Step 2 - Formatting User list

1.) `sudo touch names.txt`    

2.) `sudo nano names.txt`    

3.) Insert the names that should be formatted by namely for example:

    Aras Gill

    Amirah Mathis

    Lewys Bloom

    Marcos Halliday

# Step 3 - Generating a Custom Wordlist with Namely
- Now we must generate the wordlist with some templates to match the following

```
ESM-Example@TBHSecurity.com
FIN-Example@TBHSecurity.com
HRE-Example@TBHSecurity.com
ITS-Example@TBHSecurity.com
SEC-Example@TBHSecurity.com

```

```shell
python3 namely.py -nf names.txt -d TBHSecurity.com -t HRE-\${first1}\${last}@\${domain}
```

Example
![[Pasted image 20221031023640.png]]
In order to generate more complex user wordlists we can use the '-tf' switch to use a template file with a list of templates within it. We suggest putting your templates within a file and using the switch to automate the wordlist creation.


# Accessing Corporate Resources

In order to access Breach || GTFO, you also need to update your /etc/hosts file with a new entry to www.breachgtfo.local

Your /etc/hosts file should look like this 

    10.200.x.232    www.breachgtfo.local

    10.200.x.232    mail.corporate.local

    127.0.0.1       localhost

After adding the vhosts to your /etc/hosts file, you should now be able to access Breach || GTFO and Corporate Mail from within your browser.


## Searching and Utilizing Breached Credentials
![[Pasted image 20221031023750.png]]
After navigating to the page, you'll be presented with a web server called Breach || GTFO with a simple side menu and search bar.

Now you can combine this internal breached credentials service with the email list from leetLinked to find a potential set of valid credentials.


Our names.txt file
![[Pasted image 20221031024145.png]]

Our template file
![[Pasted image 20221031024616.png]]

Hence we get the emails as following:
```
HRE-SWinters@TBHSecurity.com
HRE-JStewart@TBHSecurity.com
HRE-RFoxx@TBHSecurity.com
HRE-YMohamed@TBHSecurity.com
HRE-CSheridan@TBHSecurity.com
HRE-SChancellor@TBHSecurity.com
HRE-MManager@TBHSecurity.com
HRE-RDennis@TBHSecurity.com
HRE-TMohlamme@TBHSecurity.com
HRE-CLopez@TBHSecurity.com
ESM-SWinters@TBHSecurity.com
ESM-JStewart@TBHSecurity.com
ESM-RFoxx@TBHSecurity.com
ESM-YMohamed@TBHSecurity.com
ESM-CSheridan@TBHSecurity.com
ESM-SChancellor@TBHSecurity.com
ESM-MManager@TBHSecurity.com
ESM-RDennis@TBHSecurity.com
ESM-TMohlamme@TBHSecurity.com
ESM-CLopez@TBHSecurity.com
FIN-SWinters@TBHSecurity.com
FIN-JStewart@TBHSecurity.com
FIN-RFoxx@TBHSecurity.com
FIN-YMohamed@TBHSecurity.com
FIN-CSheridan@TBHSecurity.com
FIN-SChancellor@TBHSecurity.com
FIN-MManager@TBHSecurity.com
FIN-RDennis@TBHSecurity.com
FIN-TMohlamme@TBHSecurity.com
FIN-CLopez@TBHSecurity.com
ITS-SWinters@TBHSecurity.com
ITS-JStewart@TBHSecurity.com
ITS-RFoxx@TBHSecurity.com
ITS-YMohamed@TBHSecurity.com
ITS-CSheridan@TBHSecurity.com
ITS-SChancellor@TBHSecurity.com
ITS-MManager@TBHSecurity.com
ITS-RDennis@TBHSecurity.com
ITS-TMohlamme@TBHSecurity.com
ITS-CLopez@TBHSecurity.com
SEC-SWinters@TBHSecurity.com
SEC-JStewart@TBHSecurity.com
SEC-RFoxx@TBHSecurity.com
SEC-YMohamed@TBHSecurity.com
SEC-CSheridan@TBHSecurity.com
SEC-SChancellor@TBHSecurity.com
SEC-MManager@TBHSecurity.com
SEC-RDennis@TBHSecurity.com
SEC-TMohlamme@TBHSecurity.com
SEC-CLopez@TBHSecurity.com
```

After trial and error of all the above emails, we got one 

![[Pasted image 20221031031120.png]]
`Password - aqAwM53cW8AgRbfr`
Username - `JStewart`


Lets spray these credentials and also try them on mail.corporate.local
![[Pasted image 20221031031546.png]]
- We get here access to Jstewarts emails

```
Hello Jeff Stewart, and welcome to Throwback Hacks Security!

As I'm sure you've already been informed, you may not have access to your network user account for a few days while IT finishes getting everything setup. In the meantime, you're able to use the Guest Account. You can access the account with the following credentials:

TBSEC_GUEST:WelcomeTBSEC1!

Note: The guest account is heavily monitored and will be deactivated as soon as your account up and running!

Thank you for your patience,

BoJack Horseman,
Information Technology Specailist
TBH{19b6ca4281bbef3ee060aaf1c2eb4021}
```


The credentials for TBSEC-DC01 (10.200.34.79) are TBSEC_GUEST:WelcomeTBSEC1!


Try to ssh, evil-winrm or RDP into the machine!

## Questions

1. What is the Users email who has been affected by the Databreach?
`SEC-JStewart@TBHSecurity.com`

2. What was the Users password?
`aqAwM53cW8AgRbfr`

3. What credentials could be found in the Email?

Format: User:Pass

`TBSEC_GUEST:WelcomeTBSEC1!`

4. Submit flags for reconnaissance in Task 4
