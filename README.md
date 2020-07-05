## Initial recon 
```
nmap -p- -sV -A -Pn 10.10.10.10
http/https_open?:
	-gobuster
	-content discovery via burp
	-wfuzz -c -w /root/xPayloads/SecLists/Discovery/Web-Content/common.txt --hc 404,403 -u "http://example.com/FUZZ.txt" -t 100
	-python3 ./dirsearch.py -u http://example.com -e *
	-cewl -w wordlists.txt -d 10 -m 1 http://example.com/
found potential user/cred?
	-try user enum on login or register
smb_open?:
	-smbclient -L //10.10.10.191
```
## linux shell todo:
spawn PTT
```
python -c 'import pty; pty.spawn("/bin/sh")'
export TERM=xterm
```
or
```
python3 -c 'import pty; pty.spawn("/bin/bash")'
export TERM=xterm
```
Look For Suids:
```
find / -perm -g=s -o -perm -4000 ! -type l -maxdepth 3 -exec ls -ld {} \; 2>/dev/null
```
Check Current user groups:
```
id 
uid=1000(ash) gid=1000(ash) groups=1000(ash),4(adm),24(cdrom),30(dip),46(plugdev),116(lxd)
```
Rest
```
sudo -l
LinEnum.sh
linuxprivchecker.py
nmap -p- 127.0.0.1
Search password in filses:
-find / -name "*backup*" 2>/dev/null
-in webapp db or config (google)
Found Zip?
```
fcrackzip -D -p rockyou test.zip
```

