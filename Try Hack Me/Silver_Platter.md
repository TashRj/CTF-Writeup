# Silverplatter Writeup CTF

### 1. Access the Target Website at 10.10.103.42

![Target Website](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20091727.png?raw=true)

---

### 2. Interesting Information Found

![Silverpeas Information](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20091807.png?raw=true)

- The username for a system called **Silverpeas** is provided.

![Silverpeas](https://github.com/user-attachments/assets/a069704e-0f26-4374-8d91-5478bc44c598)

- **Silverpeas** is a web-based tool used for collaboration among employees.

---

### 3. Run an Nmap Scan to Identify Open Ports

![Nmap Scan](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20092055.png?raw=true)

- Ports **22**, **80**, and **8080** are open.

---

### 4. Check the Silverpeas Website on Ports 80 and 8080

![Silverpeas Website](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20092313.png?raw=true)

- We successfully accessed the Silverpeas login page by visiting **http://10.10.103.42:8080/silverpeas**.

---

### 5. Check for Vulnerabilities in the Silverpeas Version (2022)

![Vulnerabilities](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20101825.png?raw=true)

- Based on the vulnerability information, we can bypass the password field and log in successfully.

---

### 6. Use Burp Suite to Intercept and Modify the Login Request

![Burp Suite Intercept](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20102059.png?raw=true)

- Open the website in Burp Suite, enable the Interceptor, and send the login request.
- Modify the username to **scr1ptkiddy** (as found earlier) and remove the password field.
- We successfully logged in to the website.

---

### 7. View the Unread Notification

![Unread Notification](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20102308.png?raw=true)

---

### 8. Enumerate Notification IDs to Find More Information

![Notification ID](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20102414.png?raw=true)

- By changing the notification ID in the URL, we can discover more messages.
- When the ID is changed to **6**, we find a message containing **SSH login credentials**.

![SSH Credentials](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20102529.png?raw=true)

---

### 9. SSH Login with the Provided Credentials

![SSH Login](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20102724.png?raw=true)

- We successfully logged into the web server using SSH.

---

### 10. Check for a Flag in the File System

![Text File](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20102815.png?raw=true)

- Using the **ls** command, we discovered a text file.
- Viewing this file reveals the **first flag**.

---

### 11. Examine `/etc/passwd` for User Information

![Passwd File](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20103031.png?raw=true)

- In the **/etc/passwd** file, we see users such as **tim** and **tyler**, but no additional interesting information here.
- Since the instructions specify that password brute-forcing with a wordlist won't work, we need to find another approach.

---

### 12. Investigate User `tim`, Who Belongs to the `adm` Group

![Adm Group](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20103735.png?raw=true)

![Adm Group Logs](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20104307.png?raw=true)

- User **tim** is part of the **adm** group, which gives access to system logs.
- We can search through the **auth.log** file for any useful information related to **tyler**.

![Auth Log](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20104349.png?raw=true)

- In the logs, we find a **database password** for **tyler**. This might be the password for **sudo** on his account.

---

### 13. Use the Database Password to Access User `tyler`'s Account

![Tyler's Account](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20104510.png?raw=true)

- We successfully logged into **tyler**'s account.

---

### 14. Escalate Privileges to Root

![Root Privileges](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20104849.png?raw=true)

- Use the **sudo su** command and enter the password to gain root access.
- Then, navigate to the **/root** directory and find a text file containing the **second flag**.

---

### 15. Conclusion

We have successfully completed the challenge and obtained both flags.

