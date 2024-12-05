# 📧 The Greenholt Phish - Portfolio Project

## Scenario
A Sales Executive at Greenholt PLC received an email that he didn't expect to receive from a customer. He claims that the customer never uses generic greetings such as "Good day" and didn't expect any amount of money to be transferred to his account. The email also contains an attachment that he never requested. He forwarded the email to the SOC (Security Operations Center) department for further investigation. 

The task is to investigate the email sample to determine if it is legitimate.

---

## 🔍 Investigation Questions and Answers

### 1. **What is the Transfer Reference Number listed in the email's Subject?**
**Answer:** 09674321  
- **Steps Taken:**  
  - I found the Transfer Reference Number in the subject line of the email.

![Screenshot](https://i.imgur.com/k9EXBmf.png)

---

### 2. **Who is the email from?**
**Answer:** Mr. James Jackson  
- **Steps Taken:**  
  - I located the sender's information in the email header. The email is from **Mr. James Jackson**.

![Screenshot](https://i.imgur.com/zHOPiee.png)

---

### 3. **What is his email address?**
**Answer:** info@mutawamarine.com  
- **Steps Taken:**  
  - The email address was visible in the "From" field of the email.

---

### 4. **What email address will receive a reply to this email?**
**Answer:** info.mutawamarine@mail.com  
- **Steps Taken:**  
  - I checked the "Reply-To" field in the email header, which shows the address that will receive a reply.

![Screenshot](https://i.imgur.com/GwTxxvw.png)

---

### 5. **What is the Originating IP?**
**Answer:** 192.119.71.157  
- **Steps Taken:**  
  - I analyzed the email headers in Mousepad and found that the originating IP is **192.119.71.157**.

![Screenshot](https://i.imgur.com/hBoIJiz.png)

---

### 6. **Who is the owner of the Originating IP?**  
**Answer:** Mutawa Marine  
- **Steps Taken:**  
  - I performed a WHOIS lookup and found the owner of the IP address **192.119.71.157** to be **Mutawa Marine**.

I verified this by visiting the following WHOIS link:  
- [WHOIS Lookup for 192.119.71.157](https://www.whois.com/whois/192.119.71.157)

![Screenshot](https://i.imgur.com/745vZfZ.png)

---

### 7. **What is the SPF record for the Return-Path domain?**
**Answer:** v=spf1 include:spf.protection.outlook.com -all  
- **Steps Taken:**  
  - I used MXToolbox to query the domain and found the SPF record to be **v=spf1 include:spf.protection.outlook.com -all**.

I checked it using this MXToolbox link:  
- [MXToolbox SPF Lookup](https://mxtoolbox.com/SuperTool.aspx?abt_id=AB-631B&abt_var=Control&run=toolpage&action=mx%3amutawamarine.com)

![Screenshot](https://i.imgur.com/zjacO9Z.png)

---

### 8. **What is the DMARC record for the Return-Path domain?**
**Answer:** v=DMARC1; p=quarantine; fo=1  
- **Steps Taken:**  
  - After using the same MXToolbox link to query the domain's DMARC record, I found it to be **v=DMARC1; p=quarantine; fo=1**.

![Screenshot](https://i.imgur.com/Y5bzi4N.png)

---

### 9. **What is the name of the attachment?**
**Answer:** SWT_#09674321____PDF__.CAB  
- **Steps Taken:**  
  - I opened the email attachment file in Mousepad and checked the Content-Type field to find the attachment name.

![Screenshot](https://i.imgur.com/eFtpyYq.png)

---

### 10. **What is the SHA256 hash of the file attachment?**
**Answer:** 2e91c533615a9bb8929ac4bb76707b2444597ce063d84a4b33525e25074fff3f  
- **Steps Taken:**  
  - I used the `sha256sum` command on my Linux system to calculate the SHA256 hash of the attachment.

![Screenshot](https://i.imgur.com/qh7UMNI.png)

---

### 11. **What is the attachment's file size?**
**Answer:** 400.26 KB  
- **Steps Taken:**  
  - I uploaded the SHA256 hash of the file to VirusTotal, which provided the file size as **400.26 KB**.

![Screenshot](https://i.imgur.com/r3wBE7M.png)

---

### 12. **What is the actual file extension of the attachment?**
**Answer:** .rar  
- **Steps Taken:**  
  - I looked at the file details in VirusTotal, where I found that the actual file extension is **.rar**.

![Screenshot](https://i.imgur.com/yx3RpWx.png)

---

## 🛠️ Tools Used  
- **Thunderbird Mail Application:** Used to open and analyze the email sample.  
- **Mousepad:** Used to examine the raw headers and file content of the email and attachment.  
- **WHOIS:** Used to determine the owner of the originating IP.  
- **MXToolbox:** For querying SPF and DMARC records for the domain.  
- **VirusTotal:** Used to analyze the SHA256 hash of the file and retrieve metadata such as file size and true extension.  
- **Linux Command-Line Tools:** Used for calculating the SHA256 hash of the attachment.  

---

## 🧠 Key Takeaways  
- Email analysis is crucial for identifying phishing attempts and validating the legitimacy of unsolicited communications.  
- Tools like WHOIS, MXToolbox, and VirusTotal are essential for identifying domain ownership, analyzing email authenticity, and examining suspicious attachments.  
- Understanding how to interpret email headers, SPF, and DMARC records helps in identifying the source and legitimacy of an email.  
