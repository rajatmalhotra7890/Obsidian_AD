# You're Five Minutes Late...

- After doing everything you can with your initial footholds, your team thinks its time to look at other resources and services that have opened while moving through the network
- Since these are internal server we will need to run through your browser through Proxychains and forward traffic through our proxy server

- We use crackmapexec again along with proxy server to find all open servers
- Run crackmapexec to see what devices are open


```shell
proxychains crackmapexec smb 10.200.34.0/24
```

We get two new machines on the network
```
10.200.34.117  -  THROWBACK-DC01
10.200.34.176  -  THROWBACK-TIME
```
- We will now run Nmap Scans against these two and save the results with other machine's scans


- We use proxychains in Firefox after performing nmap scans and discovering there is a port 80 webserver running on the server.

Now we must remember that there was an email particularly while exploring Murphyf which had a password reset link related to the THROWBACK-TIME machine
![[Pasted image 20221019140647.png]]
- We click on it and hence password is changed for murphyf to `PASSWORD` on the timekeep webserver `10.200.34.176`
![[Pasted image 20221019140730.png]]
- We reset the password for murphyf and get a flag here!
![[Pasted image 20221019140850.png]]
- We enter the credentials with the reset password `PASSWORD` and we're in as Murphyf on Throwback Timekeep machine.

## Questions
1. What is the hostname of the device?
`THROWBACK-TIME`

2. What is the title of the web page?
`Throwback Hacks Timekeep`

3. What user was the password reset for?
`MurphyF`

