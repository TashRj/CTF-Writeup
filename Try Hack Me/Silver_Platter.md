
Silverplatter writeup CTF
### 1. Go to the target website at 10.10.103.42
![Alt text](https://github.com/TashRj/CTF-Writeup/blob/main/Try%20Hack%20Me/screenshots/Screenshot%202025-02-18%20091727.png?raw=true)

### 2. We can find an interesting information here
 
The username is given for a system called Silverpeas
 
Silverpeas is a web based tool used for collaboration among employees

3. Next, run a nmap scan to view open ports
 
Port 22, 80 and 8080 are open

4. Check for the silverpeas website inside the main website for port 80 and 8080.
 
We have succesfully accessed the silverpeas login website by using 10.10.103.42:8080/silverpeas 

5. The silverpeas version is the 2022 version. We can check for any vulnarabilites during that period
 
We can remove the password form field and sucesfully login

6. On burpsuite, open the website and turn on interceptor, send a request in the login page and alter the details. Set the username to scr1ptkiddy, as found earlier and remove the password field
 
 
We have sucesfully logged in into the website

7. In the page, we have an unread notification, so lets open and view the notification
 
8. There is a message ID when checking the url of the notification, lets enumerate through the id with different numbers to find any other interesting information
 
When id is changed to 6, there is a message that provides the SSH login information


9. Lets login the SSH using the information provided
 
We have successfully logged in into the web server through ssh

10. Checking ls there is a text file present and viewing the text file would give the first flag
 





11. Viewing the /etc/passwd shows there are different users such as tim, tyler. however no and other interesting information here. And since the instruction states that password bruteforces using wordlist would not work, we have to find a different approach.
  

12. The user tim is part of the adm group, which means we can view the system logs. 
 
We can search through the auth.log for any interesting details for tyler
 

12.  
There is a database password for tyler, perhaps we can use this as the sudo password for tyler 
 
We have sucesfully entered tylers account

13.  Use sudo su command to enter as root using the same password and view cd /root where there is a text file for the second flag. And we are done 
