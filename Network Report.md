Time Thieves
You must inspect your traffic capture to answer the following questions:
What is the domain name of the users' custom site? Frank-n-Ted DC
Frank-.n-ted.com 10.6.12.12

![](Images/Wireshark%20domain%20name%20of%20user%20site.png)
![](Images/Wireshark%20user%20site%20IP.png)
![](Images/Wireshark%20ip%20dest%2010.6.12.203.png)
![](Images/traffic%20between%2010.6.12.203%20and%2010.6.12.12.png)

What is the IP address of the Domain Controller (DC) of the AD network? 10.6.12.12

What is the name of the malware downloaded to the 10.6.12.203 machine?

june11.dll

![](Images/Wireshark%20malware%20file.png)
![](Images/Wireshark%20malware%20file%202.png)

Upload the file to VirusTotal.com.

![](Images/Wireshark%20Virus%20Total.png)

What kind of malware is this classified as?

Trojan Malware

Vulnerable Windows Machine
Find the following information about the infected Windows machine:


Host name
    Rotterdam-PC
IP address
    172.16.4.205
![](Images/Wireshark%20Infected%20windows%20machine%20Host%20name%20%26%20IP.png)

MAC address
    00:59:07:b0:63:a4
![](Images/Wireshark%20Infected%20windows%20machine%20MAC.png)

What is the username of the Windows user whose computer is infected?
    matthijs.devries
![](Images/Wireshark%20username%20of%20infected%20machine.png)

What are the IP addresses used in the actual infection traffic?
172.16.4.205 was the machine that was being infected
185.243.115.84 sent many empty gif to the infected machine
166.62.111.64 was also sending high volumes of packets during the capture
![](Images/Wireshark%20IPs%20of%20actual%20infection%20traffic.png)
![](Images/Wireshark%20IPs%20of%20actual%20infection%20traffic%202.png)



