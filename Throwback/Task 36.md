Using Rubeus on TBSEC-DC01, we find kerberoastable account

![[Pasted image 20221031034021.png]]
- The service with valid SPN which was kerberoastable was `TBService`.
- We can use hashcat to crack this hash

The hash was cracked and the password is `securityadmin284650`

## We open Powershell with administrator rights and enter credentials for TBService account which has administrator rights over the machine.
Then we retrieve the root.txt flags!!!

1. What User was vulnerable to Kerberoasting?
`TBService`

2. What password could be cracked from the Kerberos Ticket?
`securityadmin284650`

3. Submit flags for TBSEC-DC01 in Task 4
