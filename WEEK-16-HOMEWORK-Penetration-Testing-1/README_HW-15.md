


> Written with [StackEdit](https://stackedit.io/).
> ## Week 16 Homework: Penetration Testing 1

### [](#scenario)Scenario

In this assignment, you will work as a recently hired security analyst at Altoro Mutual, a banking service.

-   Concerned about their online presence and the security of their website demo.testfire.net, they have hired you to evaluate the security posture of their operations.
    
-   As a holder very sensitive customer and financial data, Altoro Mutual is worried malicious actors compromising their website anf gaining this information.
    

You are tasked with performing website enumeration, discovery, and vulnerability detection. Because this engagement is non-invasive, you will **not** try to hack into their system. Rather, you will discover any potential vulnerabilities or leaks that the company should be worried about.

Please note throughout this assignment, you will target a website named "Altoro Mutual" located at `demo.testfire.net`. Altoro Mutual was designed by IBM, a company that designs both hardware and software for computers. Their website `demo.testfire.net` was specifically designed to detect web application vulnerabilities.

### [](#topics-covered-in-this-assignment)Topics Covered in This Assignment

-   Website enumeration
-   Google Dorking
-   OSINT Recon
-   Shodan
-   Recon-NG
-   Installing modules
-   Zenmap
-   nmap's scripting engine

#### [](#lab-environment)Lab Environment

You will use Azure online VMs to complete the homework.

To start the labs, log into Azure and launch the Penetration Security machine.

Once you are connected to that machine, launch the Pen Testing Hyper-V machine and start it to boot up Kali Linux.

-   Kali credentials:
    
    -   Username: `root`
    -   Password: `toor`
-   Metasploitable credentials:
    
    -   Username: `msfadmin`
    -   Password: `msfadmin`

**Note:** Your Kali machine will act as the attacker machine, and the Metasploitable machine will act as the victims machine.

Please note throughout this assignment, you will target a website named "Altoro Mutual" located at `demo.testfire.net`. Altoro Mutual was designed by IBM, a company that designs both hardware and software for computers. Their website `demo.testfire.net` was specifically designed to detect web application vulnerabilities.

### [](#instructions)Instructions:

As you complete the steps below, please record your answers in the [Submission.md file](/UCB-Coding-Bootcamp/ucb-virt-cyber-pt-06-2021-u-lol-2/-/blob/master/16-Penetration-Testing/HW/SubmissionFile.md). You will submit this file as your homework deliverable.

#### [](#step-1-google-dorking)Step 1: Google Dorking

Altoro Mutual wants to ensure that private information that is unavailable on their public website cannot be found by searching the web.

-   For example, Altoro Mutual does not mention their executive remembers on the website. Using Google, can you identify who the Chief Executive Officer?
    
-   How can this information be helpful to an attacker?**This gives an attacker a deeper understanding of the site's file structure.**
__We'll use a combination of Google search techniques to target Altoro Mutual and gather information such as:__

-   Employee email addresses
-   Employees' first and last names
-   Domain information

The goal is to find data that can be used to attack Altoro Mutual.
    

#### [](#step-2-dns-and-domain-discovery)Step 2: DNS and Domain Discovery

The reconnaissance phase of a penetration test is possibly the most important phase of the engagement. Without a clear understanding of your client's assets, vulnerabilities can go unnoticed and later exploited.

-   Navigate to `centralops.net`.
    
-   Enter the IP address for `demo.testfire.net` into Domain Dossier and answer the following questions based on the results:
    
    1.  Where is the company located?`Registrant City: Sunnyvale
Registrant State/Province: CA
Registrant Postal Code: 94085
Registrant Country: US`
        
    2.  What is the NetRange IP address?`NetRange:       65.61.137.64 - 65.61.137.127`
        
    3.  What is the company they use to store their infrastructure?` Rackspace Backbone Engineering`
        
    4.  What is the IP address of the DNS server?`65.61.137.117-AS33070-RMH-14`
        

#### [](#step-3-shodan)Step 3: Shodan

Using Shodan and the information gathered from Google Dorking, find any other useful information that can be used in an attack.

-   Navigate to [shodan.io](https://www.shodan.io/).
    
-   Run a scan against the IP address of the DNS server for `demo.testfire.net`.
    
    -   What open ports and running services did Shodan find?

#### [](#step-4-recon-ng)Step 4: Recon-ng

Altoro Mutual is also concerned about cross-site scripting attacks, which can cause havoc on their website. Verify whether or not Altoro Mutual is vulnerable to XSS by completing the following:

-   Install the Recon module `xssed`.
-   Set the source to `demo.testfire.net`.
-   Run the module.

Is Altoro Mutual vulnerable to XSS?

### [](#step-5-zenmap)Step 5: Zenmap

Your client has asked that you help identify any vulnerabilities with their file-sharing server. Using the Metasploitable machine to act as your client's server, complete the following:

-   Use Zenmap to run a service scan against the Metasploitable machine.
    
    -   **Bonus:** In the same command, output the results into a new text file named `zenmapscan.txt`.
-   Use Zenmap's scripting engine to identify a vulnerability associated with the service running on the 139/445 port from your previous scan.
    
-   Once you have identified this vulnerability, answer the following questions for your client:
    
    1.  What is the vulnerability?
    2.  Why is it dangerous?
    3.  What are your recommendations for the client to protect their server?

----------

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
