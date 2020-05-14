# Lame 

> Nashia Holloway | May 13th, 2020

## Enumeration

We have a FTP server that allows anonymous logons, SSH, and SMB open. There's also `distcc` on port `3635`, which is " a program designed to distribute compiling tasks across a network to participating hosts. It is comprised of a server, distccd, and a client program, distcc."

## Initial Access

There's nothing on the FTP server, and nothing useful came out of smbclient. I search vulnerabilities for distcc, and found `cve-2004-2687`, which allows remote code execution. There's a metasploit module that facilitates this for us, and we're able to get a shell as `daemon`. We can get the user flag under `/home/makis`.

I couldn't find a way to elevate privs, but I think it had to do with SUID bits (I need more practice with those).

## Privilege Escalation

I searched metasploit for version 3.0.20 of samba, and use the `multi/samba/usermap_script` exploit to get a shell as root and the root flag.

## Lessons Learned 

Read up on/practice suid bit exploitation
