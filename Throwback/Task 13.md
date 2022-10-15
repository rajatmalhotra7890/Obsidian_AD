# Just a Drop will do
- Your team decides that the next best move is to fire responder and try to poison LLMNR and get NTLM responses back


Explained thoroughly in `Knowledge Base\LLMNR-NBT-NS Poisoining Attack`

## Step 1 - Fire up responder in Kali instance

## Step 2 - A LLMNR/NBT-NS request will be received in the responder
- We get an LLMNR request from PetersJ with his NTLMv2 hash, which we crack using hashcat

![[Pasted image 20220930062053.png]]


## Questions

1. What User fell victim to LLMNR Poisoning?
`PetersJ`

2. What is the 4th octet of the IP Address the LLMNR request came from?
`219`

3. What is the hostname of the device?
`THROWBACK-PROD`


