# 🕵️‍♂️ TShark Challenge 2: Directory Curiosity

---

## Challenge Scenario

### Introduction  
In this challenge, I was assigned to investigate an alert triggered by a user encountering a poor file index. The investigation required inspecting the provided `directory-curiosity.pcap` file to retrieve relevant artefacts and confirm whether the alert was a true positive. I used TShark to analyze DNS queries and other traffic in the capture file, and cross-referenced findings with VirusTotal to identify any suspicious or malicious activity.

---

## ⚠️ Disclaimer  

The provided packet capture files should only be interacted with within the isolated virtual machine (VM) to ensure security.

---

## 🛠️ Task Objectives  

1. **Analyze DNS queries** in the provided `.pcap` file.  
2. **Investigate domains** using VirusTotal to identify any malicious or suspicious domains.  
3. **Extract additional artefacts** such as HTTP requests, server info, and file details to confirm the malicious nature of the domain.

---

## 🔍 Investigation Questions  

### 1. **What is the name of the malicious/suspicious domain?**  
**Answer:**  
The malicious domain identified is:  
`jx2-bavuong[.]com`
- **Steps Taken:**  
  - Ran the following TShark command to list DNS queries:  
    ```
    tshark -r dns-queries.pcap -T fields -e dns.qry.name | awk NF | sort -r | uniq -c
    ```



---

### 2. **What is the total number of HTTP requests sent to the malicious domain?**  
**Answer:**  
The total number of HTTP requests sent to the malicious domain is:  
`14`
- **Steps Taken:**  
  - Ran this TShark command to count HTTP requests related to the domain:  
    ```
    tshark -r dns-queries.pcap -T fields -e dns.qry.name -e http.request.full_uri | sort -r | uniq -c
    ```

---

### 3. **What is the IP address associated with the malicious domain?**  
**Answer:**  
The IP address associated with the malicious domain is:  
`141[.]164[.]41[.]174`
- **Steps Taken:**  
  - Ran the following command to extract the IP address associated with the domain:  
    ```
    tshark -r directory-curiosity.pcap -T fields -e http.host -e ip.addr | sort -r | uniq
    ```

---

### 4. **What is the server info of the suspicious domain?**  
**Answer:**  
The server information for the suspicious domain is:  
`Apache/2.2.11 (Win32) DAV/2 mod_ssl/2.2.11 OpenSSL/0.9.8i PHP/5.2.9`
- **Steps Taken:**  
  - Ran this TShark command to extract the server info for the malicious domain:  
    ```
    tshark -r directory-curiosity.pcap -Y "http contains \"jx2-bavuong.com\"" -T fields -e http.server
    ```

---

### 5. **What is the number of listed files in the first TCP stream?**  
**Answer:**  
The number of listed files in the first TCP stream is:  
`3`
- **Steps Taken:**  
  - Ran the following command to follow the TCP stream in ASCII and count the entries:  
    ```
    tshark -r directory-curiosity.pcap -z follow,tcp,ascii,0 -q
    ```

---

### 6. **What is the filename of the first file?**  
**Answer:**  
The filename of the first file is:  
`123[.]php`
- **Steps Taken:**  
  - Opened the `index.html` file from the captured traffic using Vim and then opened it in Firefox to view the filename.

---

### 7. **What is the name of the downloaded executable file?**  
**Answer:**  
The name of the downloaded executable file is:  
`vlauto[.]exe`
- **Steps Taken:**  
  - Created a directory and exported HTTP traffic objects:  
    ```
    mkdir export
    tshark -r directory-curiosity.pcap --export-objects http,export
    ```
  - Checked the contents of the `export` directory to find the executable.

---

### 8. **What is the SHA256 value of the malicious file?**  
**Answer:**  
The SHA256 value of the malicious file is:  
`b4851333efaf399889456f78eac0fd532e9d8791b23a86a19402c1164aed20de`
- **Steps Taken:**  
  - Ran the following command to calculate the SHA256 hash of the file:  
    ```
    sha256sum vlauto.exe
    ```

---

### 9. **What is the "PEiD packer" value from VirusTotal?**  
**Answer:**  
The "PEiD packer" value from VirusTotal is:  
`.NET executable`
- **Steps Taken:**  
  - Searched the SHA256 value of the file on VirusTotal to find this information.

---

### 10. **What does the "Lastline Sandbox" flag the file as?**  
**Answer:**  
The "Lastline Sandbox" flags the file as:  
`Under Behavior: MALWARE TROJAN`
- **Steps Taken:**  
  - Searched the SHA256 value of the file on VirusTotal to retrieve the sandbox analysis results.

---

## 🛠️ Tools Used  

- **TShark:** Used to capture, analyze, and extract DNS queries, HTTP requests, and file metadata from the packet capture.  
- **VirusTotal:** Used to analyze the domain, IP address, file hashes, and sandbox results.  
- **Command-Line Tools:** For calculating hashes and exporting traffic objects.

---

## 🧠 Key Takeaways  

- This challenge demonstrated how to use TShark to extract detailed network traffic artefacts, including DNS queries, HTTP requests, and file details.  
- VirusTotal was instrumental in confirming the malicious nature of the domain and file, as well as identifying behaviors flagged as malware.  
- The investigation emphasized the importance of analyzing traffic in depth to uncover potential threats and confirm the legitimacy of security alerts.

---



















