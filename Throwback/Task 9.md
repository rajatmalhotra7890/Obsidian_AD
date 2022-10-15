# Webshells and You!
- Your team has informed you that the pfSense box be may be running in a default configuration which makes gaining access easy. Use this information to your advantage and gain access to the pfSense configuration panel before moving on.

`This means that we could try some of the default credentials here`
`1. root:pfsense`
`2. admin:pfsense`

## pfSense Configuration Panel Overview 
- After logging into the pfSense configuration panel, we are greeted by a dashboard showing the status of the firewall. 
- This configuration panel gives us a lot of information and a lot of power. We can view and alter the way that the firewall acts as well as monitor the status of the network. 
- To use pfSense to our advantage we will look for a command prompt or web shell to execute commands and get a reverse shell on the machine.

## Finding an Attack Vector
- In order to execute commands in a web app, we first need to find our vector that executes these commands. 
- The web shell can be a command line interface directly integrated into the web server, a limited functionality shell, or a PHP command execution shell. In the case of pfSense, it can execute commands in a command prompt as well as PHP Commands. 


# My methodology to find something on pfSense configuration Panel

## Check around if you see something to play with as its literally a firewall root access you got.
- Go to `Diagnostics`  tab and see if there's a `Command Prompt` option available.
![[Pasted image 20220926024524.png]]
- Since we have Command Prompt access, we can use this to get a reverse shell!

I used PentestMonkey's PHP Reverse Shell using its Firefox extension.
![[Pasted image 20220926024733.png]]


- Thus after using netcat to catch the reverse shell, we finally have access as root!
![[Pasted image 20220926024939.png]]

Finding root.txt and flag.txt is your responsibility ;)


## Questions

1. What username was used to access the configuration portal?
`admin`

2. What password was used to access the configuration portal?
`pfsense`

3. What menu tab contains a command prompt tab in the PFSense Configuration panel?
`Diagnostics`

