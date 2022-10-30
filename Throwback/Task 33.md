# Identity Theft is Not a Joke Jim

[I have written the notes for Token Impersonation separately here](obsidian://open?vault=THM%20Networks&file=Knowledge%20Base%2FWindows%20Access%20Token%2F3.%20Token%20Impersonation%20attack)

Email Found after impersonation attack in dosierk's account in Windows
```
Hey team! Hope you guys are having a good day!

As all of you probably already now we are transferring to our new email service as we
transition please use the new emails provided to you as well as the default credentials
that can be found within your emails.

Please do not use these emails outside of corporate as they contain sensitive information.

The new email format is based on what department you are in:

ESM-Example@TBHSecurity.com
FIN-Example@TBHSecurity.com
HRE-Example@TBHSecurity.com
ITS-Example@TBHSecurity.com
SEC-Example@TBHSecurity.com

In order to access your email you will need to go to mail.corporate.local as we get our
servers moved over.

If you do not already have mail.corporate.local set in your hosts file please reach out to
IT to get that fixed.

Please remain patient as we make this transition and please feel free to email me with any
questions you may have regarding the new transition: HRE-KDoiser@TBHSecurity.com

Karen Dosier,
Human Relations Consulatant
```

Hint - Use mimikatz powershell scripts and Crackmapexec modules to do stuff remotely. This is my prep for OSCP so i am not using Metasploit for Token Impersonation Attack!


## Questions
1. What file is on the Administrator's Documents folder?
`email_update.txt`

2. Who wrote the email?
`Karen Dosier`

3. What is her official title in the company?
`Human Relations Consultant`

4. Submit flags for CORP-ADT01 in Task 4
Done!


