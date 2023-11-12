# Injecting OS commands
In this example, a shopping application lets the user view whether an item is in stock in a particular store. This information is accessed via a URL:
```bash
https://insecure-website.com/stockStatus?productID=381&storeID=29
```
To provide the stock information, the application must query various legacy systems. 
For historical reasons, the functionality is implemented by calling out to a shell command with the product and store IDs as arguments:
```bash
stockreport.pl 381 29
```
This command outputs the stock status for the specified item, which is returned to the user.
<br>
The application implements no defenses against OS command injection, 
so an attacker can submit the following input to execute an arbitrary command:
```bash
& echo aiwefwlguh &
```
If this input is submitted in the `productID` parameter, the command executed by the application is:
```bash
stockreport.pl & echo aiwefwlguh & 29
```
Next we will see this error:
```bash
Error - productID was not provided
aiwefwlguh
29: command not found
```
The three lines of output demonstrate that:
1) The original `stockreport.pl` command was executed without its expected arguments, and so returned an error message.
2) The injected `echo` command was executed, and the supplied string was echoed in the output.
3) The original argument `29` was executed as a command, which caused an error.
