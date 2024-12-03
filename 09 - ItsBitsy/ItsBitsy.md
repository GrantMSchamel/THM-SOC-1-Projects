# ItsyBitsy Lab: ELK Investigation  

In this challenge, I utilized ELK (Elasticsearch, Logstash, Kibana) to investigate a potential Command and Control (C2) communication incident. Below are the details of the investigation and findings, along with placeholders for screenshots to support each answer.   

---

## 🔍 Investigation Questions and Answers  

### 1. How many events were returned for the month of March 2022?  
**Answer:** 1,482  
- **Steps Taken:** Edited the calendar in Kibana's Discover tab to select March 1st through April 1st.  

![Screenshot for Question 1](https://i.imgur.com/rtpuGVS.png)

---

### 2. What is the IP associated with the suspected user in the logs?  
**Answer:** 192.166.65.54  
- **Steps Taken:**  
  - Searched the `source.ip` field.  
  - Identified the second most frequently used IP as the one associated with the suspected user.  

![Screenshot for Question 2](https://i.imgur.com/IIFMfrd.png)

---

### 3. The user’s machine used a legit Windows binary to download a file from the C2 server. What is the name of the binary?  
**Answer:** bitsadmin  
- **Steps Taken:**  
  - Investigated the `user_agent` field to identify the agent used by the suspected IP address.  

![Screenshot for Question 3](https://i.imgur.com/QKJASah.png)

---

### 4. The infected machine connected with a famous file-sharing site in this period, which also acts as a C2 server used by the malware authors to communicate. What is the name of the file-sharing site?  
**Answer:** pastebin.com  
- **Steps Taken:**  
  - Analyzed the logs to identify the `host` field.  
  - Found that the malware authors used this site as a C2 server.  

![Screenshot for Question 4](https://i.imgur.com/XSfzoau.png)

---

### 5. What is the full URL of the C2 to which the infected host is connected?  
**Answer:** pastebin.com/yTg0Ah6a  
- **Steps Taken:**  
  - Looked at the combination of the `host` and `uri` fields to construct the full URL.  

![Screenshot for Question 5](https://i.imgur.com/JQetGhs.png)

---

### 6. A file was accessed on the file-sharing site. What is the name of the file accessed?  
**Answer:** secret.txt  
- **Steps Taken:**  
  - Used VirusTotal to analyze the full URL.  
  - Found the file name under the "HTML Info" section in the details.  

![Screenshot for Question 6](https://i.imgur.com/KlVP6mc.png)

---

### 7. The file contains a secret code with the format THM{_____}.  
**Answer:** THM{SECRET__CODE}  
- **Steps Taken:**  
  - Accessed the file on the file-sharing site to view its contents.  

![Screenshot for Question 7](https://i.imgur.com/PZQgqF9.png)

---

## 🛠️ Tools Used  
- **ELK Stack**: Kibana for querying and analyzing logs.  
- **VirusTotal**: For analyzing URLs and files.  


