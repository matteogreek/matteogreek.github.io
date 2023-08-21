
# Alert 

```
EventID : 94
Event Time : Jun, 13, 2021, 04:23 PM
Rule : SOC147 - SSH Scan Activity
Level : Security Analyst
Source Address : 172.16.20.5
Source Hostname : PentestMachine
File Name : nmap
File Hash : 3361bf0051cc657ba90b46be53fe5b36
File Size : 2.82 MB
Device Action : Allowed
Download (Password:infected) : https://files-ld.s3.us-east-2.amazonaws.com/3361bf0051cc657ba90b46be53fe5b36.zip
```
# Analysis

Hostname: PentestMachine
IP Address: 172.16.20.5
- Terminal history: 13.06.2021 16:23 nmap -sV -sP 172.16.20.0/24
- log management: 
	- Date: Jun, 13, 2021, 04:23 PM
	- Src_IP 172.16.20.5
	- Src_port 53222
	- dest_IP 172.16.20.2
	- dest_port 22

Email: "Hi all, I will scan the LetsDefend network after 12:00 13.06.2021 This scanning could be continue all day. Please ignore SIEM alerts for "PentestMachine" hostname Hostname: PentestMachine IP Address: 172.16.20.5 Regars, Ellie"

The email from the penetration testing team indicated their intention to conduct a network scan after 12 PM. By examining the terminal history of the Pentest machine, we can observe the use of the nmap command to scan a range of IP addresses.

# Conclusion

The alert is a false positive. 


[Heartstone back home](https://matteogreek.github.io/)