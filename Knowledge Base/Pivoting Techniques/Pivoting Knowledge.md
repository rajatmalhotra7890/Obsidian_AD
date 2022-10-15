- Pivoting is the art of using access obtained over one machine to exploit another machine deeper in the network.
- Put simply, by using one of the techniques described in the following tasks (or others!), it becomes possible for an attacker to gain initial access to a remote network, and use it to access other machines in the network that would not otherwise be accessible

## Methods used in Pivoting
1. `Tunneling/Proxying`
- Creating a proxy type connection through a compromised machine in order to route all desired traffic into the targeted network.
- This could potentially also be tunneled inside another protocol (SSH tunneling) which could be useful for evading basic IDS or firewall.

2. `Port Forwarding`
- Creating a connection between local port and single port on a target, via a compromised host.



A proxy is good if we want to redirect lots of different kinds of traffic into our target network -- for example, with an nmap scan, or to access multiple ports on multiple different machines.

- `Port forwarding tends to be faster but only allows us to access a single port on a target device`


## Enumeration on a compromised machine in order to begin pivoting
- There are five possible ways to enumerate a network through a compromised host:
1. Using material found on the machine. `hosts file` or `ARP cache`
2. Using pre-installed tools.
3. Using statically compiled tools.
4. Using scripting languages.
5. Using local tools through a proxy.

1. `ARP cache`
```
arp -a
```
- This command can be used Windows or Linux to check the ARP cache of the machine and this will show you any IP addresses of the hosts the target has recently interacted with.

2. `Hosts file`
```
cat /etc/hosts

or 

type C:\Windows\System32\drivers\etc\hosts
```
- To check hosts file on each Windows or Linux environment.

3. `Identify local DNS server`
```
cat /etc/resolv.conf

or 

ipconfig /all 
```
