# Network Forensic Analysis Report

_TODO_ Complete this report as you complete the Network Activity on Day 3 of class.

## Time Thieves 
You must inspect your traffic capture to answer the following questions:

1. What is the domain name of the users' custom site?
 Domain name: Frank-n-Ted-DC. frank-n-ted.com
 wireshark filter: ip.src==10.6.12.0/24
2. What is the IP address of the Domain Controller (DC) of the AD network?
 -IP Address: 10.6.12.12 (Frank-n-Ted-DC.frank-n-ted.com)
 -Wireshark filter: ip.src==10.6.12.0/24
 ![Screenshot (274)](https://user-images.githubusercontent.com/89820505/156908635-a089cc43-cc06-4636-a1f7-7edc13c12ccb.png)
 
3. What is the name of the malware downloaded to the 10.6.12.203 machine? Once you have found the file, export it to your Kali machine's desktop.
 -Malware filename: june11.dll
 -Wireshark Filter: ip.addr == 10.6.12.0/24 
 ![Screenshot (275)](https://user-images.githubusercontent.com/89820505/156908647-a1e63567-126e-4581-8895-a8455bb54e4d.png)
 
   
4. Upload the file to [VirusTotal.com](https://www.virustotal.com/gui/). 
Exporting file to kali
 -open file tab | Export objects | select HTTP | Filter "*.dll" 
 save june.dll | Upload to virustotal.com
 
5. What kind of malware is this classified as?
 -trojan

---

## Vulnerable Windows Machine N/A

1. Find the following information about the infected Windows machine:
    - Host name
    - IP address
    - MAC address
    
2. What is the username of the Windows user whose computer is infected?
3. What are the IP addresses used in the actual infection traffic?
4. As a bonus, retrieve the desktop background of the Windows host.

---

## Illegal Downloads N/A

1. Find the following information about the machine with IP address `10.0.0.201`:
    - MAC address
    - Windows username
    - OS version

2. Which torrent file did the user download?
