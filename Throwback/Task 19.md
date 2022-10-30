# Dump it like its Hot
- Now that we have system privileges in THROWBACK-PROD, you can dump creds and attempt to pass the hash in order to gain further footholds in the network.


## Mimikatz Overview
- Mimikatz is one of the most famous tools used for dumping passwords on windows systems.
- It can be used to dump passwords with a Windows Server and mainstream Windows versions.
- However due to it being infamous, it is almost immediately picked up AV or Anti-Malware Services.
- So we must disable endpoint protection before attempting to use Mimikatz or utilize an obfuscated binary version of Mimikatz with a C2.
	- Mimikatz has many modules available like
		1. log
		2. privilege
		3. sekurlsa
		4. lsadump
		5. crypto
		6. vault
		7. token
		8. misc
		many more....

- For the sake of the lab, we will be utilizing lab, privilege, lsadump and sekurlsa


## Gaining Privilege
- Once endpoint detection is disabled, you'll need to launch mimikatz (with an Administrator level user) you'll want to type `privilege::debug` which will then put you in Debug Mode that can only be granted by an Administrator.
- From there, we will want to elevate privileges to `NT-Authority` system with `token::elevate`
- This will grant you the highest level of access that Microsoft has to offer, allowing you to do basically anything on the system, like root account on Linux system


### We know that the target is a 64 bit Windows machine
![[Pasted image 20221004114159.png]]

After transfering the mimikatz binary, we start using it.
![[Pasted image 20221004114445.png]]

Running `privilege::debug`
![[Pasted image 20221004114521.png]]
Running `token::elevate`
![[Pasted image 20221004114618.png]]

![[Pasted image 20221004114700.png]]

![[Pasted image 20221004114915.png]]

Running `lsadump::sam`
![[Pasted image 20221004115056.png]]


## Questions
Read the above and familiarize yourself with Mimikatz syntax.
