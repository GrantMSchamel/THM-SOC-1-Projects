# Investigating with Splunk 

## Scenario
SOC Analyst Johny has observed some anomalous behaviors in the logs of a few Windows machines. It looks like the adversary has access to some of these machines and successfully created a backdoor. His manager has asked him to pull those logs from suspected hosts and ingest them into Splunk for quick investigation. Our task as a SOC Analyst is to examine the logs and identify the anomalies.

---

## Questions to Answer

### 1. **How many events were collected and ingested in the index main?**
- I opened the Splunk enterprise app and used the search query `index=main`. From the results, I determined that **12,256** events were collected and ingested.

![Screenshot](https://i.imgur.com/SExGkCV.png)

---

### 2. **On one of the infected hosts, the adversary was successful in creating a backdoor user. What is the new username?**
- I filtered by the host "server" and found the event code "4720," which corresponds to user creation. I examined the event details to find that the new username was **A1berto**.

![Screenshot](https://i.imgur.com/mjcep39.png)
![Screenshot](https://i.imgur.com/F2BmPRW.png)

---

### 3. **On the same host, a registry key was also updated regarding the new backdoor user. What is the full path of that registry key?**
- I searched the logs using the new username "A1berto" and looked for EventID 13, which logs registry value changes `index=main EventID="13" "A1berto"`. I found the full path of the registry key in the details as:  
`HKLM\SAM\SAM\Domains\Account\Users\Names\A1berto\`.

![Screenshot](https://i.imgur.com/Gf2hHrg.png)

---

### 4. **Examine the logs and identify the user that the adversary was trying to impersonate.**
- By examining the "User" field in the logs, I found that the adversary was likely trying to impersonate **Alberto**, as the name appeared correctly in the logs.

![Screenshot](https://i.imgur.com/o9Iw0FW.png)

---

### 5. **What is the command used to add a backdoor user from a remote computer?**
- I searched the `index=main` logs for commands in the "CommandLine" field and found that the adversary used the following command to add the backdoor user:  
`"C:\windows\System32\Wbem\WMIC.exe" /node:WORKSTATION6 process call create "net user /add A1berto paw0rd1"`

![Screenshot](https://i.imgur.com/Xifoodh.png)

---

### 6. **How many times was the login attempt from the backdoor user observed during the investigation?**
- Using the search query `index=main A1berto`, I could not find any login attempts from the backdoor user. Similarly, searching with `index=main User="A1berto"` revealed that no login activity was logged.  
Answer: **0**

---

### 7. **What is the name of the infected host on which suspicious PowerShell commands were executed?**
- I used the search results showing the creation of the new user and traced it to a command that was executed via PowerShell. By examining the details under the "hostname" field, I found the infected host name to be **James.browne**.

![Screenshot](https://i.imgur.com/eGZgdKT.png)

---

### 8. **PowerShell logging is enabled on this device. How many events were logged for the malicious PowerShell execution?**
- I used the search query `index=main Powershell EventID=4103` to find PowerShell execution logs. In Splunk, event ID 4103 is for PowerShell logging. I found that **79** events were logged for malicious PowerShell executions.

![Screenshot](https://i.imgur.com/9bO0mMu.png)

---

### 9. **An encoded PowerShell script from the infected host initiated a web request. What is the full URL?**
- Using the information from the PowerShell logs, in order to do this we need to first use the information we got above and scroll down to find the Host Application. Next we take that info and we put it into Cyberchef. Put that code in and select “From Base64”. Then select decode text option UTF-16BE, then from there select the “From” text: aAB0AHQAcAA6AC8ALwAxADAALgAxADAALgAxADAALgA1AA== and the /news.php (extension of site)
Copy that into the input area and then decode the text from UTF-16LE. The URL used by the infected host to initiate the web request is:  
`http://10.10.10.5/news.php`

![Screenshot](https://i.imgur.com/4VnZjXy.png)

![Screenshot](https://i.imgur.com/zdGaGUS.png)

![Screenshot](https://i.imgur.com/3I8bOLa.png)


---

## 🛠️ Tools Used

- **Splunk:** For analyzing and investigating logs from the infected hosts.
- **CyberChef:** For decoding the base64-encoded PowerShell script and extracting the URL.
- **PowerShell Logs:** For identifying malicious commands executed via PowerShell.
- **Event Logs:** To track user creation, registry changes, and other suspicious activities.

---

## 🧠 Key Takeaways

- Splunk is an invaluable tool for ingesting, analyzing, and searching large volumes of log data to identify potential threats.
- Understanding event IDs and how they relate to different system activities (like user creation or registry modifications) is crucial for incident investigation.
- PowerShell is often used for malicious activities in Windows environments, so logging and monitoring PowerShell events is essential for identifying suspicious behavior.


