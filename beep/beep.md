# Beep

> Nashia Holloway | May 19th, 2020

## Enumeration

**10.10.10.7**

There's a webserver, but can't run gobuster because every page is redirected. Elastix is in the root directory. Using [this exploit](https://www.exploit-db.com/exploits/37637), we can find the pssword to login. It's also the root password for SSH. Logging in, we get root and user flags.


