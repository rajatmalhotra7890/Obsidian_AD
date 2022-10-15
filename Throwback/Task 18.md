# SEATBELT CHECK!
- You have a C2 agent responding back from THROWBACK-PROD (10.200.34.219 as PetersJ), now we need to elevate our privileges in order to dump hashes and passwords with mimikatz.
- So you team has suggested to run a script like `WinPEAS or seatbelt` to enumerate what services and privileges may be misconfigured on the device and can be exploited to escalate privileges.



## Loading and Executing Modules
- In order to run Seatbelt properly without any problems, we must run this over an RDP session

[Useful github Repo for precompiled binaries](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries) containing Rubeus.exe, Seatbelt.exe, etc.


- We can also use seatbelt module in Starkiller to help enumerate the device and find potential attack vectors.

![[Pasted image 20221004101120.png]]
- This one has optional fields so we can just run this using `Submit`.

### Note - This wont work in Starkiller rather we need a session established using RDP and then run the binary there.


## Check the Seatbelt Results Screenshots in `Miscenalleous Results/Seatbelt Binary Observations`

- Now we are interested in the `CredEnum` results which are stored within the Credentials Manager.
- We can abuse this feature to use saved creds to run a file with the account privileges.


## Exploiting Saved Credentials in Credential Manager
- Since we know that there are saved credentials within the credential manager from seatbelt, we can utilize windows `"runas"` to run a file as an elevated user and escalate privileges.
- Note -  We need an RDP session on the device in order to successfuly run this command and escalate privileges.

```powershell
runas /savecred /user:<user> /profile "cmd.exe"
```
![[Pasted image 20221004105640.png]]
- We see we get a different command prompt with elevated privileges  as user `throwback-prod\admin-petersj`
- We could also now upload a stager to this account and continue to use starkiller with a different agent with elevated privileges.


Submit the flags too!
