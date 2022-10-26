# We gotta drop the Load!

Now that we have a foothold onto the timekeep server we can being to enumerate what information we can find from the server. We can assume it is running a sql database somewhere because it had a login page. We also can assume that the web server is using xampp from the C:\ folder within the local disk. With this information we can easily find where the sql database is stored and how we can access it.


### DIY task -  Learn to enumerate SQL database 


Some Useful SQL queries for the tasks
```sql
# 1. Show all the databases after logging into the SQL database as root
show databases;

# 2. Enter into the database to further show all tables
use database;

# 3. Select all rows from database
select * from table1;

# 4. Show all tables in a database
show tables;

```


## Questions

1. What database are the timekeep login users located?
`timekeepusers`

2. What database are the domain users located in?
`domain_users`

3. What table was located in the domain users database?
`users`

4. What is the first username in the table?
`ClemonsD`

5. Submit flags for THROWBACK-TIME in Task 4.
`Answered!`


#### Miscellaneous Results

Databases
![[Pasted image 20221025144728.png]]

Tables in `timekeepusers` database
![[Pasted image 20221025144757.png]]

Entries/Records of users table in `timekeepusers`
![[Pasted image 20221025144836.png]]
```
 spopy          ilylily                                         
 foxxr          Fnfdsfdf49sA(2o1id                              
 winterss       rei0g0erggdfs(2o1id                             
 daiban         Bananas!                                        
 blairej        BlaireJ2020                                     
 FLAG           TBH{ac3f61048236fd398da9e2289622157e}           
 daviesj        FEFJdfjep302dojsdfsFSFD                          
 horsemanb      XZCFLDOSPfem,wefweop3202D                       
 peanutbutterm  fi9sfjidsJXSVNSKXKNXSIOPfpoiewspf               
 humphreyw      fedw99fjpfdsjpjpfodspjofpjf99                   
 jeffersd       fDSOKFSDFLMmxcvmxz;p[p[dgp[edfjf99              
 petersj        owowhatsthisowoDarknessBestGirlowo123uwu");      
 foxxr          ILoveAnimemes :3                                
 daviesj        efepjfjsdfjdsfpjopfdj4po                        
 gongoh         etregrokdfskggdf'fd4po                          
 dosierk        e2349efjsdsdfhgopfdj4po                          
 murphyf        PASSWORD                                        
 jstewart       e423jjfjdsjfsdj32    
```

Database domain_users
![[Pasted image 20221025145959.png]]

```
ClemonsD             
DunlopM              
LoganF               
IbarraA              
YatesZ               
CopelandS            
MckeeE               
HeatonC              
FlowersK             
HardinA              
BurrowsA             
FinneganI            
GalindoI             
LyonsC               
FullerS              
SteeleJ              
WangG                
LoweryR              
JeffersD             
GreigH               
SharpK               
KruegerM             
ChenI                
VillanuevaD          
BegumK    
```
- Now that we have got domain users we can use crackmapexec for password spraying against Domain Controller machine and see if any logon is successful!

Password list used:
```
Summer2020
Management2018
7eQgx6YzxgG3vC45t5k9
SinonFTW123!
```