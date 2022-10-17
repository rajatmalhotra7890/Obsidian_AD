# Yo Dawg, I heard you like proxies. 
- Your team has informed you that Throwback Hacks has taken on some good security practices and are properly segmenting their network resources.
- Now that you have a couple of footholds onto the network, you can utilize them as proxy server to pivot and access internal resources.


### What is Pivoting?
- In a good network, often referred to as a "Segmented Network", there are certain rules in place preventing users from accessing certain parts of internal LAN (example is the Workstation subnet must not be accessible to the Server subnet). 
- This is a headache for pentesters as most networks are not segmented, these networks are referred to as `"Flat Networks"`.
- To make segmented networks more like flat networks we use tools such as `Proxychains` or `SShuttle` or even `chisel` which make it easier to compromise other subnets of the LAN and pivot from one subnet in a LAN to another.

[Pivoting with Chisel](obsidian://open?vault=THM%20Networks&file=Knowledge%20Base%2FPivoting%20Techniques%2F3.%20Chisel)


## Questions

Read the above and setup your proxy

