# 🛠️ Eviction: APT28 Investigation  

Sunny, a SOC analyst at E-corp, investigates potential threats from APT28, a group targeting organizations similar to E-corp. Using the MITRE ATT&CK Navigator, Sunny analyzes the TTPs (Tactics, Techniques, and Procedures) of APT28 to identify potential network intrusions and mitigate threats. Below are the findings and investigation details.  

---

## 🖥️ Lab Setup  

- **Organization:** E-corp  
- **Threat Group:** APT28  
- **Tool Used:** [MITRE ATT&CK Navigator](https://attack.mitre.org)  

---

## 🔍 Investigation Questions and Answers  

### 1. What is a technique used by the APT to both perform recon and gain initial access?  
**Answer:** Spearphishing link  
- **Details:**  
  - This technique is used to gather reconnaissance on employees through phishing emails and gain initial access when a user clicks the malicious link.  

![Screenshot for Question 1](https://i.imgur.com/FFX94fJ.png)

---

### 2. Which accounts might the APT compromise while developing resources?  
**Answer:** Email accounts  
- **Details:**  
  - APT28 commonly uses email accounts to distribute phishing links, making them likely targets during the resource development phase.  

![Screenshot for Question 2](https://i.imgur.com/464bmJy.png)

---

### 3. What two techniques of user execution should Sunny look out for?  
**Answer:** Malicious File and Malicious Link  
- **Details:**  
  - APT28 might trick users into executing malicious code by clicking on infected files or links distributed through social engineering tactics.  

![Screenshot for Question 3](https://i.imgur.com/xm3UB0J.png)

---

### 4. If the above technique was successful, which scripting interpreters should Sunny search for to identify successful execution?  
**Answer:** Powershell and Windows Command Shell  
- **Details:**  
  - APT28 is likely to use these scripting interpreters to gain deeper access and execute commands on the compromised systems.  

![Screenshot for Question 4](https://i.imgur.com/QGDWv7q.png)

---

### 5. Which registry keys should Sunny observe to track persistence changes made by obfuscated scripts?  
**Answer:** Registry Run Keys  
- **Details:**  
  - Registry Run Keys allow malicious scripts to copy themselves into the startup directory, enabling persistence on the machine.  

![Screenshot for Question 5](https://i.imgur.com/BR4JYeo.png)

---

### 6. Which system binary's execution should Sunny scrutinize for proxy execution?  
**Answer:** Rundll32  
- **Details:**  
  - This Windows binary is used to execute DLLs containing executable code, enabling APT28 to hide malicious commands and evade detection.  

![Screenshot for Question 6](https://i.imgur.com/HltqhzT.png)

---

### 7. Which technique might the APT be using when Sunny identified `tcpdump` on a compromised host?  
**Answer:** Network Sniffing  
- **Details:**  
  - `tcpdump` is a tool for capturing and analyzing network traffic, used by APT28 to discover sensitive data and network activity.  

![Screenshot for Question 7](https://i.imgur.com/YJftzub.png)

---

### 8. Which remote services should Sunny observe to identify APT activity traces?  
**Answer:** SMB/Windows Admin Shares  
- **Details:**  
  - APT28 may exploit these services to move laterally and gain administrative access to remote systems.  
  - Reference: [T1021.002 - SMB/Windows Admin Shares](https://attack.mitre.org/techniques/T1021/002/)  

![Screenshot for Question 8](https://i.imgur.com/D968bt4.png)

---

### 9. Which information repository is the likely target for intellectual property theft?  
**Answer:** SharePoint  
- **Details:**  
  - SharePoint is used by companies to store sensitive information, making it a prime target for APT28's intellectual property theft operations.  

![Screenshot for Question 9](https://i.imgur.com/8IhHmCR.png)

---

### 10. What types of proxy might the APT use for data exfiltration?  
**Answer:** External Proxy and Multi-hop Proxy  
- **Details:**  
  - **External Proxy:** Used to retrieve data without a direct internet connection, often through port redirection or cloud-based resources.  
  - **Multi-hop Proxy:** Routes traffic through multiple servers to encrypt data and hide the IP, increasing anonymity and evasion.  

![Screenshot for Question 10](https://i.imgur.com/tFRvLvZ.png)

---

## 🛠️ Tools Used  

- **MITRE ATT&CK Navigator:** For identifying APT28's TTPs.  
- **tcpdump:** Detected for potential network sniffing activities by APT28.  
- **Windows Command Shell and Powershell:** Commonly used scripting interpreters for execution.  

---

## 🧠 Key Takeaways  

- Proactively monitoring phishing techniques and user accounts is critical in mitigating initial access attempts.  
- Registry Run Keys and system binaries like `Rundll32` can serve as indicators of persistence and proxy execution tactics.  
- Tools like `tcpdump` and remote services exploitation (e.g., SMB/Windows Admin Shares) are crucial areas to scrutinize during lateral movement investigations.  


