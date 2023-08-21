# Summary

This exercise is about a suspicious Chrome extension named "ChatGPT for Google. The alert was triggered due to the suspicious addition of the extension to the browser, indicating a potential security threat. The add-on, disguising as a ChatGPT tool, targeted users' Facebook profiles. Despite its removal from the Chrome Web Store, many had already installed it, posing concerns about data privacy. Subsequent checks of network activity showed links to harmful websites related to the extension's C2 framework. These links, combined with data from threat intelligence sources, verified the extension's malevolent intent and the significant danger it presented to users.
# Alert 

```
Severity: High
Type: Data Leakage
EventID : 153
Event Time : May, 29, 2023, 01:01 PM
Rule : SOC202 - FakeGPT Malicious Chrome Extension
Level : Security Analyst
Hostname : Samuel
IP Address : 172.16.17.173
File Name : hacfaophiklaeolhnmckojjjjbnappen.crx
File Path : C:\Users\LetsDefend\Download\hacfaophiklaeolhnmckojjjjbnappen.crx
File Hash : 7421f9abe5e618a0d517861f4709df53292a5f137053a227bfb4eb8e152a4669
Command Line : chrome.exe --single-argument C:\Users\LetsDefend\Download\hacfaophiklaeolhnmckojjjjbnappen.crx
Trigger Reason : Suspicious extension added to the browser.
Device Action : Allowed
```

From the alert details given, a dubious file has been identified on a system labeled "Samuel" having an IP address of 172.16.17.173. This alert was activated by the SOC202 rule pertaining to the FakeGPT Malicious Chrome Extension. From the provided data, it seems the command line is trying to access or modify a Chrome extension file (having a .crx extension) via the Google Chrome browser. The device's response is labeled as "allowed", suggesting that the device didn't intervene or halt the file's execution.

The file name of the extension added to the browser is: **hacfaophiklaeolhnmckojjjjbnappen.crx** 
The file hash is: **7421f9abe5e618a0d517861f4709df53292a5f137053a227bfb4eb8e152a4669**
# Analysis

In the following segment, we'll delve into a comprehensive examination of the flagged malicious extension, utilizing external tools and methods. Moreover, we are going to try to identify the Command and Control (C2) address associated with the malware.
## Extension Analysis

- Virustotal: No security vendors and no sandboxes flagged this file as malicious
- MalwareBazaar: No results
- ChromeStats: https://chrome-stats.com/d/hacfaophiklaeolhnmckojjjjbnappen
	Using ChromeStats we can find some interesting information. The extension is flagged as malicious and was removed from the Web Store. This is could be a sign that the extension is actually malicious and the alert is a true positive one. 

![Pasted image 20230819163706](https://github.com/matteogreek/matteogreek.github.io/assets/70201797/69054b95-0c81-4312-a4e8-e2c091e66c53)


By looking at the Browse History of the affected Host "Samuel" using the EDR,  we can see that he visited the URL: https://chrome.google.com/webstore/detail/chatgpt-for-google/hacfaophiklaeolhnmckojjjjbnappen at 2023-05-29 13:01:44. Visiting the URL, resulted in a 404 error message. This finding seems to agree with the previous clue obtained with ChromeStats.

## Command and Control (C2) Identification

In this section, we will search for signs of Command and Control (C2) access. Let's start by analyzing the network-related logs gathered from the "Samuel" Host.

On the Log Management tab we can filter by Samuel's IP address 172.16.17.173.
Here we find that the source IP made:
- a request to the IP 52.76.101.124 on port 80 on May, 29, 2023, 01:02 PM. By analyzing the raw log entry we can see that the Hostname linked to the destination IP is www.chatgptforgoogle.pro. 
- Another request was made to IP 172.217.17.142 on port 80 on May, 29, 2023, 01:03 PM (1 min after the previous one). By analyzing the raw log entry we can see that the Hostname linked to the destination IP is chrome.google.com
- Another request was made to IP 18.140.6.45 on port 80 on May, 29, 2023, 01:03 PM (1 min after the previous one). By analyzing the raw log entry we can see that the Hostname linked to the destination IP is www.chatgptgoogle.org
- A DNS Query was made:  
	- QueryResult: ::ffff:104.21.63.166;::ffff:172.67.147.243;
	- QueryName: version.chatgpt4google.workers.dev
 
Further investigation of the domain www.chatgptforgoogle.pro on threat intelligence platforms, such as VirusTotal, confirms its malicious nature.

# Conclusion

The alert was a true positive and the findings confirm that the Chrome extension is malicious.
Furthermore the Host accessed the malicious C2 address and so it was isolated from the network.


[Heartstone back home](https://matteogreek.github.io/)