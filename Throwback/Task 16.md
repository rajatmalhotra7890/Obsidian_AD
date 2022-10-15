# Deploy The Grunts
- We will begin our movement through the network with our second with our second foothold on `THROWBACK-PROD` 
- Your team has informed you that the best plan of attack is to plant a C2 agent into the THROWBACK-PROD and attempt to escalate privileges before assessing another footholds and laterally moving through the network.



## Uploading a C2 agent with Starkiller
- Starkiller uses a listener and stager to create an agent the listener does exactly as it sounds like, it listens on a given port for a connection back from your agent.
- The stager is like a payload you send to the target to get an agent back


## Creating Listeners in Starkiller
![[Pasted image 20221004094701.png]]
- Deploy a listener on Starkiller with any port binding and your tun0 interface IP address.


## Creating and Uploading a Stager using Starkiller
![[Pasted image 20221004094818.png]]
- Click on `Create`

Select the type of stager as `windows/launcher_bat`

Now download it locally and use powershell on victim machine (PetersJ) to transport it from your local machine to the remote machine (target)

![[Pasted image 20221004095042.png]]


## After executing the stager, we get a callback from the machine on our Starkiller listener
![[Pasted image 20221004100039.png]]
