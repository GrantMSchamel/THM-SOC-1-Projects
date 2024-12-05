# 🖥️ Monday Monitor - Portfolio Project

## Scenario
Swiftspend Finance, a leading fintech company, is enhancing its cybersecurity measures to protect its customers and digital assets. As part of their efforts, they are testing endpoint monitoring using Wazuh and Sysmon. Senior Security Engineer John Sterling is leading the project, and they've invited me to help investigate the logs from an April 29, 2024, test. During this test, I was tasked with identifying suspicious processes and network connections from the logs generated between 12:00:00 and 20:00:00. My role as a cyber sleuth is to analyze these logs and provide valuable insights to help strengthen Swiftspend's defenses.

---

## 🔍 Investigation Questions and Answers

### 1. **Initial access was established using a downloaded file. What is the file name saved on the host?**
**Answer:** SwiftSpend_Financial_Expenses.xlsm  
- **Steps Taken:**  
  - I started by searching for HTTP events in the logs, which led to identifying the downloaded file. I found that the file downloaded to the host was **SwiftSpend_Financial_Expenses.xlsm**.  

![Screenshot](https://i.imgur.com/3FoCrLy.png)  
![Screenshot](https://i.imgur.com/xiEdSs7.png)

---

### 2. **What is the full command run to create a scheduled task?**
**Answer:**  
`"cmd.exe" /c "reg add HKCU\SOFTWARE\ATOMIC-T1053.005 /v test /t REG_SZ /d cGluZyB3d3cueW91YXJldnVsbmVyYWJsZS50aG0= /f & schtasks.exe /Create /F /TN "ATOMIC-T1053.005" /TR "cmd /c start /min \"\" powershell.exe -Command IEX([System.Text.Encoding]::ASCII.GetString([System.Convert]::FromBase64String((Get-ItemProperty -Path HKCU:\\SOFTWARE\\ATOMIC-T1053.005).test)))" /sc daily /st 12:34"`  
- **Steps Taken:**  
  - I searched for "schtasks.exe" in the logs to find instances of scheduled task creation. I identified the command that created the task and found it in the `parentCommandLine` field.  

![Screenshot](https://i.imgur.com/PiCZoto.png)

---

### 3. **What time is the scheduled task meant to run?**
**Answer:** 12:34  
- **Steps Taken:**  
  - The scheduled task was set to run at **12:34**, which I identified in the command used to create the task.  

![Screenshot](https://i.imgur.com/xi0eGxx.png)

---

### 4. **What was encoded?**
**Answer:**  
The encoded Base64 string `cGluZyB3d3cueW91YXJldnVsbmVyYWJsZS50aG0=` was decoded to reveal a command to ping:  
`www[.]youarevulnerable[.]thm`  
- **Steps Taken:**  
  - I noticed the presence of the `FromBase64String` method in the command. The encoded Base64 string was extracted, and I used CyberChef to decode it.  

![Screenshot](https://i.imgur.com/NcXRjS8.png)  
![Screenshot](https://i.imgur.com/wOkueyr.png)

---

### 5. **What password was set for the new user account?**
**Answer:** I_AM_M0NIT0R1NG  
- **Steps Taken:**  
  - I searched the logs for "net1" and found several related events. After reviewing the details, I identified that the password set for the new user account was **I_AM_M0NIT0R1NG**.  

![Screenshot](https://i.imgur.com/hm7rJEr.png)

---

### 6. **What is the name of the .exe that was used to dump credentials?**
**Answer:** memotech.exe  
- **Steps Taken:**  
  - I searched for "mimikatz," a tool commonly used for credential dumping. I found that the program **memotech.exe** was used to dump credentials.  

![Screenshot](https://i.imgur.com/NrsaJ7A.png)

---

### 7. **Data was exfiltrated from the host. What was the flag that was part of the data?**
**Answer:** THM{VulnerableFlag}  
- **Steps Taken:**  
  - To find the flag that was part of the exfiltrated data, I searched for the term **THM**, which led me to identify the flag. I did more research on this and discovered that the command used in this scenario is a common command for PowerShell to send data to a Pastebin API to create a new paste containing sensitive data.  

![Screenshot](https://i.imgur.com/qFJ4Pte.png)

---

## 🛠️ Tools Used  
- **Wazuh & Sysmon:** For endpoint monitoring and log collection.  
- **CyberChef:** For decoding Base64-encoded strings.  
- **PowerShell & Windows Logs:** For identifying commands and scheduled tasks.  
- **CommandLine & Event Logs:** For examining user activity, credential dumping, and file downloads.  

---

## 🧠 Key Takeaways  
- Endpoint monitoring tools like Wazuh and Sysmon are crucial for detecting suspicious activity and tracking potential intrusions.  
- Scheduled tasks and PowerShell commands can be used by attackers to maintain persistence and execute malicious activities.  
- Credential dumping tools such as mimikatz can be used to harvest passwords, and it's important to monitor for such activities.  
- Investigating logs and correlating different events can provide valuable insights into potential attack vectors and exfiltration attempts.  
