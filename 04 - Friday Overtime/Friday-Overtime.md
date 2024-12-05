# 🕵️‍♂️ Friday Overtime: Malware Analysis Challenge

---

## Challenge Scenario

### Introduction  
It's a Friday evening at PandaProbe Intelligence when a notification appears on your CTI platform. While most are already looking forward to the weekend, you realise you must pull overtime because SwiftSpend Finance has opened a new ticket, raising concerns about potential malware threats. The finance company, known for its meticulous security measures, stumbled upon something suspicious and wanted immediate expert analysis.

As the only remaining CTI Analyst on shift at PandaProbe Intelligence, you quickly took charge of the situation, realising the gravity of a potential breach at a financial institution. The ticket contained multiple file attachments, presumed to be malware samples.

With a deep breath, a focused mind, and the longing desire to go home, you began the process of:

1. Downloading the malware samples provided in the ticket, ensuring they were contained in a secure environment.  
2. Running the samples through preliminary automated malware analysis tools to get a quick overview.  
3. Deep diving into a manual analysis, understanding the malware's behaviour, and identifying its communication patterns.  
4. Correlating findings with global threat intelligence databases to identify known signatures or behaviours.  
5. Compiling a comprehensive report with mitigation and recovery steps, ensuring SwiftSpend Finance could swiftly address potential threats.

---

## ⚠️ Disclaimer  

The artefacts in this scenario were retrieved from a **real-world cyber-attack**. Interaction with these files should be done **only within the isolated virtual machine (VM)** provided to ensure a secure environment.  

---

## 🛠️ Task Objectives  

1. **Download and analyze suspicious malware samples.**  
2. **Identify the malware's behavior and communication patterns.**  
3. **Correlate findings with global threat intelligence.**  
4. **Compile a detailed report with mitigation and recovery strategies.**  

---

## 🖥️ Setup and Access  

### Connecting to the VM  
1. Start the VM in split-screen mode by clicking the **Start Machine** button.  
2. Use the following credentials to access the **DocIntel platform**:  
   - **Username:** ericatracy  
   - **Password:** Intel321!  
3. **Note:** The platform may display "Connection Refused" initially, as it takes a few minutes to fully start.

---

## 🔍 Investigation Questions  

### 1. **Who shared the malware samples?**  
**Answer:** Oliver Bennett  
- **Steps Taken:**  
  - Reviewing the provided documentation revealed that the malware samples were shared by Oliver Bennett.

![Screenshot Placeholder](https://i.imgur.com/wSXpvMY.png)

---

### 2. **What is the SHA1 hash of the file pRsm.dll inside samples.zip?**  
**Answer:** 9d1ecbbe8637fed0d89fca1af35ea821277ad2e8  
- **Steps Taken:**  
  - **Command Used:** sha1sum pRsm.dll

![Screenshot Placeholder](https://i.imgur.com/WPK0wqS.png)

---

### 3. **Which malware framework utilizes these DLLs as add-on modules?**  
**Answer:** MgBot  
- **Steps Taken:**  
  - Research revealed that these DLLs are utilized as add-on modules in the MgBot malware framework.

![Screenshot Placeholder](https://i.imgur.com/Ch00tvE.png)

---

### 4. **Which MITRE ATT&CK Technique is linked to using pRsm.dll in this malware framework?**  
**Answer:** T1123 - Audio Capture  
- **Steps Taken:**  
  - Analysis identified that pRsm.dll relates to the T1123 (Audio Capture) technique in the MITRE ATT&CK framework.

![Screenshot Placeholder](https://i.imgur.com/Euvvmyi.png)

---

### 5. **What is the CyberChef defanged URL of the malicious download location first seen on 2020-11-02?**  
**Answer:** hxxp[://]update[.]browser[.]qq[.]com/qmbs/QQ/QQUrlMgr_QQ88_4296.exe

![Screenshot Placeholder](https://i.imgur.com/ICTcakO.png)
![Screenshot Placeholder](https://i.imgur.com/SEnrCzs.png)

---

### 6. **What is the CyberChef defanged IP address of the C&C server first detected on 2020-09-14 using these modules?**  
**Answer:**  122[.]10[.]90[.]12  
- **Steps Taken:**  
  - This IP was identified as the Command & Control (C&C) server.

![Screenshot Placeholder](https://i.imgur.com/6dOIJZH.png)
![Screenshot Placeholder](https://i.imgur.com/A2gMT6X.png)

---

### 7. **What is the SHA1 hash of the SpyAgent family spyware hosted on the same IP targeting Android devices on November 16, 2022?**  
**Answer:** 1c1fe906e822012f6235fcc53f601d006d15d7be  
- **Steps Taken:**  
  - This hash was retrieved from VirusTotal by analyzing the IP's relations and digging into the details of the hosted spyware.

![Screenshot Placeholder](https://i.imgur.com/LQB08iH.png)
![Screenshot Placeholder](https://i.imgur.com/SaRxemW.png)

---

## 🛠️ Tools Used  

- **VM (Virtual Machine):** Used to securely analyze malware samples.  
- **CyberChef:** For defanging URLs and IPs.  
- **VirusTotal:** For researching malware hashes and related information.  
- **Command-Line Tools:** Used for extracting file hashes and running malware samples.  

---

## 🧠 Key Takeaways  

- The scenario mimics a real-world cyber-attack investigation, providing hands-on experience with malware analysis and threat intelligence.  
- Key tools like CyberChef, VirusTotal, and command-line tools were used to analyze the malware and correlate findings with known threat data.  
- Understanding and applying MITRE ATT&CK techniques is essential for identifying and mitigating advanced persistent threats (APT) effectively.
