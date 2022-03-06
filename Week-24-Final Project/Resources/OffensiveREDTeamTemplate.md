# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services
Netdiscover results identift the IP addresses of Targets on the network: 
netdiscover -r 192.168.1.255/16

Nmap scan results for each machine reveal the below services and OS details:
Name of VM: Target 1
OS: Linux
Purpose: Defensive blue team
IP addresss: 192.168.1.110



$ nmap -sV 192.168.1.110 
  
  
-


This scan identifies the services below as potential points of entry:
- Target 1
  Port 22/tcp open ssh (service) OpenSSH 6.7p1 Debian 5+deb8u4
Port 80/tcp open http (service) Apache httpd 2.4.10 ((Debian))
Port 111/tcp open rpcbind (service) 2-4 (RPC #100000)
Port 139/tcp open netbios-ssn (services) Samba smbd 3.X - 4.X
Port 445/tcp open netbios-ssn (services) Samba smbd 3.X - 4.X

CVE-2021-28041 open SSH
CVE-2017-15710 Apache https 2.4.10
CVE-2017-8779 exploit on open rpcbind port could lead to remote DoS
CVE-2017-7494 Samba NetBIOS

The following vulnerabilities were identified on each target:
- Target 1
  - List of Critical Vulnerabilities
-Network Mapping and User Enumeration (WordPress site)
-Weak User Password
-MySQL Database Access
-MySQL Data Exfiltration
-Misconfiguration of User Privileges/Privilege Escalation

![Screenshot (267)](https://user-images.githubusercontent.com/89820505/156906545-8b6f6c6d-540d-4300-bd0c-f79bed0be889.png)

### Exploitation
-Enumerated wordpress site users w/ WPscan to obtain username michael used SSH to get user shell
-Command used: wpscan --url http://192.168.1.110/wordpress --eu
![WPscan)](https://user-images.githubusercontent.com/89820505/156906779-d60a937c-90bf-454d-9977-f4d2da116cae.png)
![WPscan.2](https://user-images.githubusercontent.com/89820505/156906833-c94cd189-c934-4b72-b7aa-6f33f03bb367.png)
![WPscan.3](https://user-images.githubusercontent.com/89820505/156906839-30ee85d5-4dad-49e4-9de7-2a624f253bfe.png)

Can visit the IP address of the target 192.168.1.110 over HTTP port 80

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`: flag1{b9bbcb33e11b80be759c4e844862482d}
    - **Exploit Used**
      - _TODO: ssh into Michael's account and look in the /var/www files_
      - the username and password michael were the same allowing for ssh connection (big vulnerability)
      - command: cd /var/www | ls | grep -RE flag html
  - `flag2.txt`: _TODO: flag2{fc3fd58dcdad9ab23faca6e9a36e581c}
    - **Exploit Used**
      - ssh into Michael's account and look in the /var/www files
      - command: cd /var/www | ls -lah | cat flag2.txt_
