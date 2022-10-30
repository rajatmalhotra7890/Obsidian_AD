# Building Your Own Dark... er Deathstar
- Now that we have footholds onto the network we need to begin to setup a command and control to gain persistence as well as escalate privileges.


So far, we have accomplished the following
```
Foothold no-1 - THROWBACK-WS01 (BlaireJ through Phishing on mail server)
10.200.34.222

Foothold no-2 - THROWBACK-PROD (PetersJ through LLMNR posioning)
10.200.34.219

Also we compromised the THROWBACK-MAIL (10.200.34.232)  server by sending out phishing emails too 

Also on top of that, we got access to pfSense firewall software hosted on THROWBACK-FW01 (10.200.34.138) (root user using Firewall Diagnostics Panel)
```

![[Pasted image 20220930144021.png]]



## What is Command and Control (C2)?
- In simple words, this is just an interface to upload and control various post exploitation tools without interacting with the target itself.
- Consider C2 as a means for mass-management of exploited targets for further usage - be it lateral movement, information gathering and so on..


For this we are going to be using
1. Powershell Empire (the fork from BC-Security)
2. Starkiller (which acts as GUI/frontend for Empire C2)


`DIY Task -  Install Powershell Empire C2 and Starkiller`


## Step 1 - Start Empire C2 
```shell
sudo ./empire --rest
```

## Step 2 - Start starkiller
```shell
sudo ./starkiller-x.x.x.AppImage --no-sandbox
```

Login Credentials for Starkiller
```
uri: 127.0.0.1:1337

user: empireadmin

pass: password123
```

We will see the following screen/UI on Starkiller after logging in
![[Pasted image 20220930144710.png]]


## Questions
Read the above text and install Starkiller
