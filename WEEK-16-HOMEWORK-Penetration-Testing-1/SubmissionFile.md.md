## Week 16 Homework Submission File: Penetration Testing 1

#### Step 1: Google Dorking


- Using Google, can you identify who the Chief Executive Officer of Altoro Mutual is:
-   ![16-1A](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK-16-HOMEWORK-Penetration-Testing-1/IMAGES/hw16-1A.PNG)

- How can this information be helpful to an attacker:
- **This gives an attacker a deeper understanding of the site's file structure.**
__We'll use a combination of Google search techniques to target Altoro Mutual and gather information such as:__


#### Step 2: DNS and Domain Discovery

Enter the IP address for `demo.testfire.net` into Domain Dossier and answer the following questions based on the results:

  1. Where is the company located:
   `Registrant City: Sunnyvale
Registrant State/Province: CA
Registrant Postal Code: 94085
Registrant Country: US`


  3. What is the NetRange IP address:
 `NetRange:       65.61.137.64 - 65.61.137.127`

  5. What is the company they use to store their infrastructure:
  ` Rackspace Backbone Engineering`


  7. What is the IP address of the DNS server:
`65.61.137.117-AS33070-RMH-14`
![16-2-4](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK-16-HOMEWORK-Penetration-Testing-1/IMAGES/2-4.PNG)
#### Step 3: Shodan

- What open ports and running services did Shodan find:
    - ![16-3B](C:%5CUsers%5Chjavid%5CPictures%5CForHW-15%5C16-HW)
    - ![16-3A](C:%5CUsers%5Chjavid%5CPictures%5CForHW-15%5C16-HW)

#### Step 4: Recon-ng

- Install the Recon module `xssed`. 
- Set the source to `demo.testfire.net`. 
- Run the module. 

Is Altoro Mutual vulnerable to XSS: 
__YES, as shown in the pictures below__

_![16-A](C:%5CUsers%5Chjavid%5CPictures%5CForHW-15%5C16-HW)
-![16-B](C:%5CUsers%5Chjavid%5CPictures%5CForHW-15%5C16-HW)
### Step 5: Zenmap

Your client has asked that you help identify any vulnerabilities with their file-sharing server. Using the Metasploitable machine to act as your client's server, complete the following:

- Command for Zenmap to run a service scan against the Metasploitable machine:
- `nmap -sV 192.168.0.10` 
 
- Bonus command to output results into a new text file named `zenmapscan.txt`:
- `nmap -sV -sC -oN zenmapscan.txt 192.168.0.10` 
- ![16-5-a](C:%5CUsers%5Chjavid%5CPictures%5CForHW-15%5C16-HW)

- Zenmap vulnerability script command: 
- `nmap --script samba-vuln-cve-2012-1182 192.168.0.10 `
- 

- Once you have identified this vulnerability, answer the following questions for your client:
  1. What is the vulnerability:
__On port 139 and 445, the Samba version is " Samba smbd 3.0.20-Debian" (pic16-5-B),  and Samba version 3.6.3 and all version previous to this are affected by a vulnerability that allows remote code execution as the "root" user from an anonymous connection. and that version has vulnerabilities as picture below:__
![16-5-B](C:%5CUsers%5Chjavid%5CPictures%5CForHW-15%5C16-HW)
![16-5-C](C:%5CUsers%5Chjavid%5CPictures%5CForHW-15%5C16-HW)
  2. Why is it dangerous:  __The version is old and not uppdated, and that version has vulnerabilities as picture below:__
![16-5-E](C:%5CUsers%5Chjavid%5CPictures%5CForHW-15%5C16-HW)
  3. What mitigation strategies can you recommendations for the client to protect their server:
  __Services have to be updated to latest version__
  __Anonymous connection must be edited in config__
  __Hardenning remote connection to ssh/keys and remove root privilege for remote connection__
  

---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  

