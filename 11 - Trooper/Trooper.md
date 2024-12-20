# Trooper - Portfolio Project  

## Introduction: Threat Intelligence Analysis  
As a Cyber Threat Intelligence (CTI) analyst, I conducted an investigation to identify the Tactics, Techniques, and Procedures (TTPs) employed by a threat group targeting a multinational technology company. Leveraging platforms such as OpenCTI and the MITRE ATT&CK Navigator, I gathered actionable insights into the adversary’s identity, malware, and attack methods.  

This project showcases my ability to use threat intelligence platforms and frameworks to identify and map advanced persistent threats (APTs).  

---

## 🔍 Investigation Questions and Answers  

### 1. **What kind of phishing campaign does APT X use as part of their TTPs?**  
**Answer:** Spear-phishing attacks  
- **Steps Taken:**  
  - Analyzed the provided threat advisory report.  
  - Identified that the group employs spear-phishing techniques to target victims, a common method for obtaining initial access.  

![Screenshot](https://i.imgur.com/w0KnGFH.png)

---

### 2. **What is the name of the malware used by APT X?**  
**Answer:** USBferry  
- **Steps Taken:**  
  - Searched for APT X in OpenCTI.  
  - Located a link to the malware associated with this threat group, revealing the name USBferry.  

![Screenshot](https://i.imgur.com/1Y3JToE.png)

---

### 3. **What is the malware's STIX ID?**  
**Answer:** malware--5d0ea014-1ce9-5d5c-bcc7-f625a07907d0  
- **Steps Taken:**  
  - Navigated to the USBferry malware profile in OpenCTI.  
  - Found the STIX ID listed under the basic information section for the malware.  

![Screenshot](https://i.imgur.com/jYtBdOI.png)

---

### 4. **With the use of a USB, what technique did APT X use for initial access?**  
**Answer:** Replication Through Removable Media  
- **Steps Taken:**  
  - Reviewed the advisory report and analyzed APT X’s methods in OpenCTI.  
  - Identified the use of USB devices to propagate malware in air-gapped environments.  
  - Cross-referenced this behavior with the MITRE ATT&CK framework and confirmed the technique.  

![Screenshot](https://i.imgur.com/QRQDRPp.png)

---

### 5. **What is the identity of APT X?**  
**Answer:** Tropic Trooper  
- **Steps Taken:**  
  - Searched for USBferry malware in OpenCTI.  
  - Navigated to the “Intrusion Sets” tab under its knowledge base, revealing the threat group identity as Tropic Trooper.  

![Screenshot](https://i.imgur.com/GnKoYMz.png)

---

### 6. **On OpenCTI, how many Attack Pattern techniques are associated with the APT?**  
**Answer:** 39  
- **Steps Taken:**  
  - Viewed Tropic Trooper’s knowledge base in OpenCTI.  
  - Accessed the “Distribution of Relations” section to find the number of attack patterns associated with this APT.  

![Screenshot](https://i.imgur.com/DCZjaib.png)

---

### 7. **What is the name of the tool linked to the APT?**  
**Answer:** BITSAdmin  
- **Steps Taken:**  
  - Under the Tropic Trooper knowledge base in OpenCTI, selected the “Tools” tab.  
  - Found BITSAdmin listed as one of the tools associated with the threat group.  

![Screenshot](https://i.imgur.com/HKHQ84K.png)

---

### 8. **Load up the Navigator. What is the sub-technique used by the APT under Valid Accounts?**  
**Answer:** T1078 Valid Accounts: Local Accounts  
- **Steps Taken:**  
  - In the MITRE ATT&CK Navigator, searched for Tropic Trooper.  
  - Reviewed techniques under “Valid Accounts” and identified Local Accounts as the relevant sub-technique.  

![Screenshot](https://i.imgur.com/6y9Bh6b.png)

---

### 9. **Under what Tactics does the technique above fall?**  
**Answer:** Defense Evasion, Persistence, Privilege Escalation, Initial Access  
- **Steps Taken:**  
  - Selected the T1078 technique in the MITRE ATT&CK Navigator.  
  - Viewed its description page to find the associated tactics listed on the right side.  

![Screenshot](https://i.imgur.com/CZKLgfO.png)

---

### 10. **What technique is the group known for using under the tactic Collection?**  
**Answer:** Automated Collection  
- **Steps Taken:**  
  - Returned to OpenCTI and navigated to Tropic Trooper’s knowledge base.  
  - Selected the “Attack Patterns” tab under the “Collection” tactic and identified Automated Collection as the technique used.  

![Screenshot](https://i.imgur.com/SVvFppQ.png)

---

## Timeline of Events  

1. The company identified cyber attacks targeting intellectual property and operations.  
2. Threat reports and CTI tools were used to investigate the TTPs of APT X.  
3. The group employed spear-phishing campaigns to distribute the USBferry malware.  
4. Tropic Trooper was identified as the threat group targeting Taiwan, The Philippines, and Hong Kong.  
5. Techniques such as Replication Through Removable Media and Automated Collection were uncovered.  

---

## 🛠️ Tools and Techniques  

- **OpenCTI:** To gather information on malware, threat actors, and associated techniques.  
- **MITRE ATT&CK Navigator:** To map TTPs and link them to specific tactics and sub-techniques.  
- **Threat Report Analysis:** For understanding adversary behavior and goals.  

---

## 🧠 Key Takeaways  

- Threat intelligence platforms are essential for identifying adversaries’ attack patterns.  
- Mapping TTPs to the MITRE ATT&CK framework provides a structured view of threats.  
- CTI investigations involve correlating multiple sources to build a comprehensive threat profile.  
