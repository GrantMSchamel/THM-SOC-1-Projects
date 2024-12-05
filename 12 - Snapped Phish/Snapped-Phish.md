# Snapped Phish-ing Line - Portfolio Project

## Introduction: Phishing Campaign Investigation  
As an IT personnel for SwiftSpend Financial, I was tasked with investigating a widespread phishing campaign targeting employees. Several employees reported receiving suspicious emails, and some had already submitted their credentials to the phishing page. My responsibilities included analyzing the emails, investigating the phishing URLs, retrieving and dissecting the phishing kit, and leveraging Cyber Threat Intelligence (CTI) tools to gather more information about the adversary.  

This project highlights my ability to investigate phishing campaigns and secure an organization against credential theft.

---

## 🔍 Investigation Questions and Answers  

### 1. **Who is the individual who received an email attachment containing a PDF?**  
- **Answer:** William McClean  
  I reviewed the emails in the `phish-emails` folder and identified William McClean as the recipient of the PDF attachment.  

![Screenshot](https://i.imgur.com/76BZ7Ey.png)

---

### 2. **What email address was used by the adversary to send the phishing emails?**  
- **Answer:** `Accounts.Payable@groupmarketingonline.icu`  
  This was retrieved by inspecting the email headers and the "From" address in the phishing emails.  

![Screenshot](https://i.imgur.com/9WHJvuf.png)

---

### 3. **What is the redirection URL to the phishing page for Zoe Duncan? (defanged format)**  
- **Answer:**  
  **`hxxp[://]kennaroads[.]buzz/data/Update365/office365/40e7baa2f826a57fcf04e5202526f8bd/?email=zoe[.]duncan@swiftspend[.]finance&error`**  
  By examining Zoe Duncan’s phishing email, I located the redirection URL embedded in the message.  

![Screenshot](https://i.imgur.com/sqt0p60.png)

---

### 4. **What is the URL to the .zip archive of the phishing kit? (defanged format)**  
- **Answer:**  
  **`hxxp[://]kennaroads[.]buzz/data/Update365[.]zip`**  
  The phishing kit was identified in the `/data` directory of the domain.  

![Screenshot](https://i.imgur.com/3DUauKo.png)

---

### 5. **What is the SHA256 hash of the phishing kit archive?**  
- **Answer:**  
  **`ba3c15267393419eb08c7b2652b8b6b39b406ef300ae8a18fee4d16b19ac9686`**  
  After downloading the `.zip` file, I used the `sha256sum` command to calculate the hash.  

![Screenshot](https://i.imgur.com/88xaMja.png)

---

### 6. **When was the phishing kit archive first submitted?**  
- **Answer:** 2020-04-08 21:55:50 UTC  
  This information was retrieved from VirusTotal by searching the SHA256 hash under "First Submission."  

![Screenshot](https://i.imgur.com/auCr7gt.png)

---

### 7. **When was the SSL certificate for the phishing domain first logged?**  
- **Answer:** 2020-06-25  
  By searching for the domain in VirusTotal, I found the earliest SSL certificate in the Historical SSL Certificates section.  

![Screenshot](https://i.imgur.com/vKsfUql.png)

---

### 8. **What was the email address of the user who submitted their password twice?**  
- **Answer:** michael.ascot@swiftspend.finance  
  By analyzing the `log.txt` file from the phishing kit directory, I identified Michael Ascot's email being submitted multiple times.  

![Screenshot](https://i.imgur.com/rlXCxgC.png)

---

### 9. **What was the email address used by the adversary to collect compromised credentials?**  
- **Answer:** `m3npat@yandex.com`  
  In the `submit.php` file within the phishing kit, I found the attacker’s email address where credentials were sent.  

![Screenshot](https://i.imgur.com/bUVKvvw.png)

---

### 10. **What is the email address that ends in "@gmail.com"?**  
- **Answer:** `jamestanner2299@gmail.com`  
  Using the `grep` command, I searched for Gmail addresses within the phishing kit and identified this one.  

![Screenshot](https://i.imgur.com/jlGoaQ9.png)

---

### 11. **What is the hidden flag?**  
- **Answer:** `THM{pL4y_w1Th_tH3_URL}`  
  I found the flag at the URL `http://kennaroads.buzz/data/Update365/office365/flag.txt`. It was encoded in Base64 (`fUxSVV8zSHRfaFQxd195NExwe01IVAo=`), and I decoded it using CyberChef.  

![Screenshot](https://i.imgur.com/HlA00Kq.png)

---

## Timeline of Events  

1. Employees received phishing emails with malicious links.  
2. Some employees submitted their credentials to the phishing site.  
3. The phishing kit was hosted on `kennaroads.buzz`.  
4. Credentials were sent to the attacker’s email addresses (`m3npat@yandex.com`, `jamestanner2299@gmail.com`).  
5. Logs indicated repeated credential submissions from a compromised employee.  
6. The phishing kit was analyzed to extract indicators of compromise (IOCs).  
7. A hidden flag was found in the phishing kit.  

---

## 🛠️ Tools and Techniques  

- **Email Header Analysis:** To trace sender information and phishing URLs.  
- **VirusTotal:** For gathering intelligence on malicious files and domains.  
- **CyberChef:** For decoding Base64-encoded data.  
- **Command-Line Tools:** For hashing (`sha256sum`) and searching (`grep`).  
- **Web Browsing (in VM):** To safely analyze phishing URLs.  

---

## 🧠 Key Takeaways  

- Analyzing phishing kits and emails provides valuable insight into attackers’ tactics.  
- CTI tools like VirusTotal are crucial for identifying IOCs and understanding adversaries.  
- Ensuring safe practices, such as using isolated environments, is critical for handling malicious artifacts.  
- Thorough investigation can uncover multiple attack vectors and secure organizational defenses.  
