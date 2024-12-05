# Unattended - Portfolio Project  

## Introduction  
Welcome to my investigation of a potential data exfiltration incident. The scenario involves a suspicious janitor spotted near an employee's office, raising concerns about unauthorized user activity during the employee's absence. My task was to uncover any unauthorized access or file exfiltration that occurred between **12:05 PM to 12:45 PM on November 19, 2022**.  

The investigation utilized disk image analysis and specialized tools provided on the system. Confidentiality was maintained throughout, adhering to strict NDA requirements.  

---

## Questions and Answers  

### 1. **What file type was searched for using the search bar in Windows Explorer?**  
- I analyzed the `NTUSER.DAT` file using Registry Explorer. Navigating to `WordWheelQuery` under:  
  **Software -> Microsoft -> Windows -> CurrentVersion -> Explorer**  
  revealed the searched file type:  
  **`.pdf`**  

![Screenshot](https://i.imgur.com/f767GBb.png)

---

### 2. **What top-secret keyword was searched for using the search bar in Windows Explorer?**  
- By inspecting the `TypedPaths` and `WordWheelQuery` registry keys, and decrypting data using the Data Inspector tool, I found the keyword searched:  
  **Continental**  

![Screenshot](https://i.imgur.com/Qu19xqZ.png)

---

### 3. **What is the name of the downloaded file to the Downloads folder?**  
- Using Autopsy, I added the disk image from the `kape-results` directory as a data source and filtered web download activity for the specified timeframe.  
  **File Name:** `7z2201-x64.exe`  

![Screenshot](https://i.imgur.com/D1zpkIh.png)

---

### 4. **When was the file from the previous question downloaded?**  
- Timestamp found in Autopsy:  
  **2022-11-19 12:09:19 UTC**  

![Screenshot](https://i.imgur.com/ffeeWku.png)

---

### 5. **Thanks to the previously downloaded file, a PNG file was opened. When was this file opened?**  
- In Registry Explorer, searching for `.png` under the `RecentDocs` path revealed the timestamp:  
  **2022-11-19 12:10:21 UTC**  

![Screenshot](https://i.imgur.com/ffeeWku.png)

---

### 6. **A text file was created in the Desktop folder. How many times was this file opened?**  
- Using `JLECmd`, a tool for parsing shell item metadata, I identified the text file's interaction count:  
  **2 times**  

![Screenshot](https://i.imgur.com/8B0UNqK.png)

---

### 7. **When was the text file from the previous question last modified?**  
- Timestamp extracted from `JLECmd` output:  
  **2022-11-19 12:12 UTC**  

![Screenshot](https://i.imgur.com/8B0UNqK.png)

---

### 8. **The contents of the file were exfiltrated to pastebin.com. What is the generated URL of the exfiltrated data?**  
- Reviewing web history in Autopsy revealed the Pastebin URL:  
  **https://pastebin.com/1FQASAav**  

![Screenshot](https://i.imgur.com/a8bGO4B.png)

---

### 9. **What is the string that was copied to the Pastebin URL?**  
- Located in Autopsy under `Data Artifacts`, the exfiltrated string was:  
  **ne7AIRhi3PdESy9RnOrN**  

![Screenshot](https://i.imgur.com/KvkMIWM.png)

---

## Timeline of Events  

1. **12:09:19 UTC:** A file (`7z2201-x64.exe`) was downloaded to the system.  
2. **12:10:21 UTC:** A PNG file was opened using the downloaded software.  
3. **12:12 UTC:** A text file was created on the Desktop and interacted with twice.  
4. **12:13 UTC:** Contents of the text file were exfiltrated to Pastebin (`https://pastebin.com/1FQASAav`).  

---

## 🛠️ Tools Used  

- **Registry Explorer:** For analyzing registry keys like `WordWheelQuery` and `TypedPaths`.  
- **Autopsy:** To review recent activity, including web downloads and history.  
- **JLECmd:** For extracting interaction metadata from shell items.  

---

## 🧠 Key Takeaways  

- This investigation highlights the importance of registry analysis and forensic tools in detecting unauthorized activity.  
- Autopsy and command-line utilities like `JLECmd` provide critical insights into user behavior and data exfiltration.  
- Maintaining security awareness and auditing unusual behavior is crucial in preventing similar incidents.  

