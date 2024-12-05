# 🕵️‍♂️ TShark Challenge 1: Traffic Analysis Investigation

---

## Challenge Scenario

### Introduction  
In this challenge, I was tasked with investigating suspicious traffic data as part of a Security Operations Center (SOC) team. The investigation was prompted by an alert from the threat research team, which flagged a potentially malicious domain. I used TShark and VirusTotal to analyze the provided packet capture (`teamwork.pcap`) and extract key indicators of compromise (IoCs).

The objectives were:
- To analyze the suspicious domain in the captured traffic.
- To identify the malicious domain, its IP address, submission details, and other artifacts.
  
Tools used: **TShark**, **VirusTotal**

---

## ⚠️ Disclaimer  

The traffic data provided in this challenge contains real examples. Interaction with the traffic data should only occur within the isolated virtual machine (VM) provided to ensure a secure environment.

---

## 🛠️ Task Objectives  

1. **Analyze the captured traffic** using TShark to identify suspicious domains and activity.  
2. **Use VirusTotal** to cross-reference findings and gather additional metadata.  
3. **Extract and document key indicators of compromise (IoCs)** such as domain names, IP addresses, and email addresses.  

---

## 🔍 Investigation Questions  

### 1. **What is the full URL of the malicious/suspicious domain address?**  
**Answer:**  
The full malicious URL identified is:  
`www.paypal.com4uswebappsresetaccountrecovery.timeseaways.com`

- **Steps Taken:**  
  - Ran the following TShark command to extract HTTP hostnames:  
    ```
    tshark -r teamwork.pcap -T fields -e http.host | sort -r | uniq
    ```


---

### 2. **When was the URL of the malicious/suspicious domain address first submitted to VirusTotal?**  
**Answer:**  
The URL was first submitted to VirusTotal on:  
`2017-04-17 22:52:53 UTC`
- **Steps Taken:**  
  - Investigated the VirusTotal entry for the domain and retrieved submission details.


---

### 3. **Which known service was the domain trying to impersonate?**  
**Answer:**  
The domain was attempting to impersonate:  
`PayPal`
- **Steps Taken:**  
  - Correlated the domain and URL with known service names.

---

### 4. **What is the IP address of the malicious domain?**  
**Answer:**  
The IP address identified for the malicious domain was:  
Defanged format: `192[.]168[.]1[.]100`
- **Steps Taken:**  
  - Used the following TShark command to extract IP addresses from POST requests:  
    ```
    tshark -r teamwork.pcap -Y "http.request.method == POST" -T fields -e ip.addr
    ```


---

### 5. **What is the email address that was used?**  
**Answer:**  
The email address found in the captured traffic was:  
Defanged format: `johnny5alive[at]gmail[.]com`
- **Steps Taken:**  
  - First, filtered POST requests with TShark to create a new capture file:  
    ```
    tshark -r teamwork.pcap -Y "http.request.method == POST" -w analyst.pcap
    ```
  - Then, extracted the email address from the file using this command:  
    ```
    tshark -r analyst.pcap -T fields -e http.file_data -e urlencoded-form.key -e urlencoded-form.value
    ```

---

## 🛠️ Tools Used  

- **TShark:** Used for capturing and analyzing network traffic to extract relevant data.  
- **VirusTotal:** Used to investigate the domain and IP address for any malicious activity.  
- **Command-Line Tools:** Used for filtering traffic, extracting specific data, and creating new capture files.

---

## 🧠 Key Takeaways  

- This challenge provided a practical example of using TShark to analyze network traffic and identify malicious domains.  
- Leveraging VirusTotal helped to confirm the malicious nature of the domain and provided additional metadata for further investigation.  
- Extracting IoCs like IP addresses and email addresses is crucial for building a comprehensive picture of the malicious activity and preventing future threats.

---  




























