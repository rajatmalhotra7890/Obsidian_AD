## What is #LLMNR and NBT-Name Service?
- LLMNR also knows as Link-Local Multi-Cast Name Resolution while NBT-NS is known as NetBIOS Name service.
- These are used in Windows Domain Network environment to identify host addresses on a network when DNS resolution fails.
	- LLMNR and NBT-NS are enabled by default on Windows computers.


When a user requests a name resource, the name of the resource must be resolved to an IP address so that user's computer knows where to send the network traffic.

- To resolve the name, user's computer will try to take the following actions in order or priority:
1. Check if the name resolves to a computer itself
2. Check to see if the resource name is in the cache or manually specified in system host's file (C:\\Windows\\System32\\drivers\\etc\\hosts)
3. Send a lookup request to configured DNS server.
4. Broadcast an LLMNR name query to all machines on local network.
5. Broadcast an NBT-NS request to all machines on local network.

`These LLMNR and NBT-NS queries will be sent to all the hosts on local network asking them to respond if they know the IP address of hostname being queried. Attackers can exploit this and will respond with their own IP address to direct subsequent network traffic for requested resource to their own machine`

LLMNR Intro
```
LLMNR was (is) a protocol used that allowed name resolution without the requirement of a DNS server. It was (is) able to provide a hostname-to-IP based off a multicast packet sent across the network asking all listening Network-Interfaces to reply if they are authoritatively known as the hostname in the query.  It does this by sending a network packet to port UDP 5355 to the multicast network address (all layer 2).
```


## How does NBT-NS and LLMNR poisoning work?
- To begin the attack, start an LLMNR/NBT-NS poisoner such as Responder.
- Responder can listen for NBT-NS and LLMNR queries being broadcast on the local network and by default also set up several different servers, most notably SMB.
	- These will be used to receive authentication requests after the poisoning.

```
python Responder.py -I eth0 -rdvw
```

You can see below that while listening for events, Responder has picked up an LLMNR query and has proceeded to poison these requests.

![[Pasted image 20220927065318.png]]
- These LLMNR queries were not for any service that could be useful to an attacker, however if someone mistypes the file share name on one of the Windows domain machines on network, the victim computer will now attempt to authenticated to the malicious spoofed share which doesnt exist.

![[Pasted image 20220927065535.png]]
If we now check back with Responder, we can see that the authentication negotiation has taken place and we have now captured username and NetNTLMv2 (NTLMv2) hash.

![[Pasted image 20220927065609.png]]

Moving forward, we can do the following:
1. Crack NTLM/NTLMv2 hashes in order to gain access to user accounts
2. SMB Relay attack 