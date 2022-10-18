- Kerberos is a network authentication protocol
- It is designed to provide strong authentication for client/server applications by using secret-key cryptography (asymmetric cryptography)

Kerberos has the following characteristics:-
1. Secure - It never sends a password unless its encrypted.
2. Only a single login required per session - Credentials defined at the login are then passed between resources without the need for additional logins.
3. It depends on the trusted third party - a Key Distribution Center (KDC). KDC is aware of all systems in the network and is trusted by all of them.
4. It performs mutual authentication - where client proves its identity to a server and server proves its identity to the client.


### Kerberos introduces the conept of a Ticket Granting Server (TGS)
- A client that wishes to use the service has to receive a ticket -  a time limited cryptographic message - giving access to the server.
- Kerberos also requires an Authentication Server to verify the clients requesting for tickets.
- These two servers - 1.) TGS 2.) AS make up the entire KDC

![[Pasted image 20221017202536.png]]

## Step 1 - AS-REQ
- The user logs on to the workstation and requests service on the host
- The workstation sends a message to Authorization Server requesting a TGT

In this step, a time stamp encrypted with the user's password is also sent so that KDC would decrypt it and verify the timestamp.


## Step 2 - AS-REP
- The Authorization server verifies the user's access rights in the user database and creates a TGT (encrypted with the TGS Secret key) and a TGS session key
- The AS encrypts the results using a key derived from user's password and sends a message back to the user workstation
- The workstation prompts the user for a password and uses the password to decrypt the incoming message.
- When decryption succeeds, the user will be able to request a TGT for a service ticket


## Step 3 - TGS-REQ
- When the user wants access to a service, the workstation client application sends a request to Ticket Granting Service containing:
1. Client name
2. Real name
3. Timestamp

- The user proves his identity by sending an authenticator encrypted with TGS session key received in step 2

User now sends three messages in total to TGS
1. TGT (with TGS Session key in it added)
2. Attributes like ServiceName/ID and requested lifetime for the TGT
3. User authenticator message containing Username/ID and timestamp, encrypted with TGS session key


## Step 4 - TGS-REP
- The TGS decrypts the ticket and ticket authenticator, verifies the request, and creates a service ticket for the requested server.
- The ticket contains the client name and optionally the client IP address.
- It also maintains the realm name and ticket lifespan.
- The TGS returns the Service Ticket to the user workstation.
	- The returned message contains two copies of a server session key 
		1. One encrypted by client password
		2. Second encrypted by service password


#### In detail
1. The TGS decrypts the TGT with the TGS Secret key and obtain the TGS session key which it will be using to decrypt the User Authenticator message containing the timestamp and UserName/ID.
	- Now TGS matches and performs validation if the username in TGT and User authenticator, timestamps in both TGT and User Authenticator, compares IP addresses too and also Lifetime of TGT.
	- This all validation is perfomed by the Ticket Granting Server/Service

2. Now the TGS creates a Service ticket for the service requested by the user/client containing:
		1. UserName/ID
		2. ServiceName/ID
		3. Timestamp
		4. User IP
		5. Lifetime for Service Ticket
		6. Service Session Key (placed in both Attributes message and Service ticket)

The TGS sends 2 messages in total back to the client including the Service ticket for the service requested:
1. Attributes message containing 1.) ServiceName/ID 2.) Timestamp 3.) Lifetime (same as TGT), encrypted with TGS Secret key
2. Service ticket, encrypted with Service Secret key

Both these messages are sent to the user


## Step 5 - AP-REQ
- Now the user receives the Service Ticket and another message including the Service Session key and other attributes
- Now the client creates a new authenticator message containing the username/ID and the timestamp, encrypted with Service Session Key which was received in the first message in Step 4.


So user simply forwards 2 messages to the Service including the Service Ticket:
1. User Authenticator, encrypted with the Service Session Key
2. Service Ticket, encrypted with Service Secret Key



## Step 6 - AP-REP
- The Service after receiving the Service Ticket, now decrypts the Service Ticket with the help of Service Secret Key and gets hold of the Service Session Key
- The Service will then use this symmetric Service Session Key to decrypt the contents of Authenticator Message sent by the user/client.
	- Then Service verifies details of the user from Service Ticket, compares timestamps from both the messages.


- Now the service after verifying everything about the Service Ticket, sends a Service Authenticator message to the Client for the client to verify if he/she is talking to a legitimate service.

The authenticator message is encrypted with the Service Session Key containing
1. ServiceName/ID
2. Timestamp


Now the client decrypts the authenticator message, encrypted with symmetric Service Session Key and thus completes the mutual authentication