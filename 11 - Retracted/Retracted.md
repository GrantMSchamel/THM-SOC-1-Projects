# Retracted - Portfolio Project

## Introduction: A Mother's Plea  
A distressed call led me to investigate a ransomware attack on a personal computer. Your mother Sophie, had unknowingly downloaded and executed a malicious installer. After noticing encrypted files and a ransom note on her desktop, she reached out for help. By the time I arrived, the ransom note had been replaced with a message to check a Bitcoin wallet. My task was to uncover what happened and ensure the computer's security.

---

## Questions to Answer  

### 1. **What is the full path of the text file containing the "message"?**  
- I used File Explorer to trace the creation of the ransom note. The file path was:  
  **`C:\Users\Sophie\Desktop\SOPHIE.txt`**  

![Screenshot](https://i.imgur.com/kDA4aNC.png)

---

### 2. **What program was used to create the text file?**  
- The program used was **notepad.exe**.

![Screenshot](https://i.imgur.com/35GKv5w.png)

---

### 3. **What is the time of execution of the process that created the text file?**  
- By filtering the logs in Sysmon for text file creations, I determined the time of execution as:  
  **2024-01-08 14:25:30 UTC**  

![Screenshot](https://i.imgur.com/OLYBPBG.png)

---

### 4. **What is the filename of this "installer"? (Including the file extension)**  
- Searching through the logs in the time frame before this text file was created, I used the Find feature for file downloads which revealed the installer file as:  
  **`antivirus.exe`**  

![Screenshot](https://i.imgur.com/cOwuiV7.png)

---

### 5. **What is the download location of this installer?**  
- The installer was downloaded to:  
  **`C:\Users\Sophie\download`**

![Screenshot](https://i.imgur.com/c3TqlDy.png)

---

### 6. **The installer encrypts files and then adds a file extension to the end of the file name. What is this file extension?**  
- The malware appended the file extension **`.dmp`** to encrypted files, such as:  
  **`C:\Users\Sophie\Desktop\VolunteerContacts - 2.xlsx.dmp`**  

![Screenshot](https://i.imgur.com/gTEHV0y.png)

---

### 7. **The installer reached out to an IP. What is this IP?**  
- I searched for network connection logs and identified the destination IP as:  
  **`10.10.8.111`**  

![Screenshot](https://i.imgur.com/6kbTPT9.png)

---

### 8. **The threat actor logged in via RDP right after the "installer" was downloaded. What is the source IP?**  
- The source IP for the RDP login was identified in the logs:  
  **`10.13.27.93`**  

![Screenshot](https://i.imgur.com/Uflaf3z.png)

---

### 9. **This other person downloaded a file and ran it. When was this file run?**  
- Reviewing download activity, the file was executed at:  
  **2024-01-08 14:24:18 UTC**  

![Screenshot](https://i.imgur.com/AM0wJnV.png)

---

## Timeline of Events  

1. Sophie downloaded and executed the malicious installer (`antivirus.exe`).  
2. The malware encrypted files and displayed a ransom note on the desktop.  
3. Sophie reached out for help after noticing the changes.  
4. A threat actor logged into the system via RDP using IP `10.10.8.111`.  
5. The intruder downloaded and ran a decryption tool, restoring the files.  
6. The ransom note was replaced with a text file instructing Sophie to check her Bitcoin wallet.  
7. I arrived and began investigating the incident.  

---

## 🛠️ Tools Used  

- **Windows Event Viewer:** For analyzing process creation and network activity logs.  
- **Sysmon:** To trace detailed process and file activity.  
- **PowerShell:** To search logs and filter events efficiently.  

---

## 🧠 Key Takeaways  

- Ransomware attacks can encrypt files quickly, leaving little time to react.  
- Tools like Sysmon and Event Viewer are essential for reconstructing attack timelines.  
- Network monitoring is critical for identifying unauthorized remote access.  
- End users need cybersecurity training to recognize malicious downloads and avoid executing suspicious files.

