# Wallace and Gromit
- Now that you have a stable foothold onto THROWBACK-WS01 your team has informed you that it maybe best to enumerate what is going on the workstation from the shells that you might have gotten from phishing and pfsense logs as well as a new shell from pass the hash.

```powershell
Invoke-BloodHound -CollectionMethod All -ZipFileName loot.zip -Domain Throwback.local
```

[Refer to this for Bloodhound Guide](obsidian://open?vault=THM%20Networks&file=Knowledge%20Base%2FTools%2F2.%20Bloodhound)
[Cheatsheet for Bloodhound](obsidian://open?vault=THM%20Networks&file=Knowledge%20Base%2FTools%2FBloodhound%20Cheatsheet.pdf)

### Step 1 - First transfer the script `SharpHound.ps1` to blairej.THROWBACK or any other domain user.
- Keep in mind that SharpHound must be run a domain user's context, but not in local user or local admin's context.
![[Pasted image 20221016114815.png]]

`Note -  The credentials for blairej were gathered by mimikatz as one of the logged on users so use that password or pass-the-hash using evil-winrm`


### Step 2 - Now ssh or use evil-winrm session shell or even RDP if its enabled.
- Import the module 
- Run the command to run Bloodhound
```powershell
Invoke-BloodHound -CollectionMethod All -ZipFileName blood.zip -Domain THROWBACK.local
```


### Step 3 -  Now use scp to transfer files
```shell
scp blairej@10.200.34.219:C:\/Users\/blairej.THROWBACK.local\/Downloads\/blood.zip /path/local
```



## Now upload the data collected by SharpHound ingestor and feed it to BloodHound!


#### Results
1. `Kerberoastable Accounts`
![[Pasted image 20221016123612.png]]

2. `Kerberoastable Users with most privileges`
![[Pasted image 20221016123654.png]]

3. `Map All Domain Admins`
![[Pasted image 20221016125018.png]]
- Click on all nodes here and see different privileges these domain admins have.
- Lots of useful info can be found out from these nodes

![[Pasted image 20221016125204.png]]

![[Pasted image 20221016125223.png]]

![[Pasted image 20221016125247.png]]
- This user is a member of the following groups as well.

`First degree Local admins rights of Hans Mercer`
![[Pasted image 20221016125341.png]]
- So this is an important info as hans mercer (mercerh) is a local admin on the domain controller


`Derivative Local admin rights`
![[Pasted image 20221016125447.png]]

`First Degree RDP privileges`
![[Pasted image 20221016125546.png]]


## Questions
1. What service account is kerberoastable? 
`sqlservice`

2. What domain does the trust connect to?
`CORPORATE.local`

3. What normal user account is a domain admin?
`mercerh`

