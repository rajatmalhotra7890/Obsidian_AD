# So anyways, I Just Started Hiring

- From the email on CORP-ADT01 we know that corporate emails are moving to a new email format,we also know a proprietary breached credentials service that we can utilize to find credentials on the network.
	- Using Linkedin along with `LeetLinked` we can pull emails and names from Linkedin to format with namely and insert into Breach || GTFO


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

## OSINT with Linkedin
- LeetLinked is a tool to automate discovery of emploiyees Linkedin Accounts.
- By discovering all employees of an organization, we can use those emails for password spraying, phishing or other targeted attacks
- It has a built in feature to generate emails based off a given format, which we can use to password spray, phish or lookup their email in a databreach.
- The optional `-p` flag uses HaveIBeenPwned API to query each email and enumerate databreaches the victim email has been a part of.


### Pulling off info from Linkedin using LeetLinked
- Recon tool used to gather employees at a company by utilizing search engines like Google and Bing.
- The results are returned in an Excel Sheet

We need HaveIBeenPwned API keys and Dehashed API keys so the combination of the tool along with these two data breach sources can be an effective red team ops tool.


![[Pasted image 20221031021013.png]]


What we need to write in shell to use the tool appropriately
```shell
python3 leetlinked.py -e 'throwback.local' -f 1 "Throwback hacks"
```

Thus now we get a list of employee names and their emails
![[Pasted image 20221031022007.png]]



## Questions
Read the above and use leetLinked to gather info from LinkedIn.



