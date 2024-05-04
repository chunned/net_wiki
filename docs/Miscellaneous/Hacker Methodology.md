[Source](https://tryhackme.com/r/room/hackermethodology)

## Reconnaissance 
Reconnaissance is the process of gathering information about a target. Generally, it does not involve interaction with the target. 

Reconnaissance might involve Googling a company to learn about its history or tools it uses, reading its Wikipedia, or the company's social media. 

Examples of recon tools:

-   **Google (specifically Google Dorking)**
-   **Wikipedia**
-   **PeopleFinder.com**
-   **who.is**
-   **sublist3r**
-   **hunter.io**
-   **builtwith.com**
-   **wappalyzer**

## Enumeration and Scanning
This phase involves directly interacting with the target to gather information about it. It involves more specialized tools and produces more useful results. The goal of this phase is to define and narrow the **attack surface**. 

Examples of enumeration/scanning tools:
- **Nmap**
- **Gobuster**
- **Metasploit**
- **exploit-db**
- **Burp Suite**
## Exploitation
This phase is when the knowledge gained in recon and enumeration is actually used to access the machine.

Examples of exploit tools:
- **Metasploit**
- **Burp Suite**
- **SQLMap**
- **BeEF**

## Privilege Escalation
After access to the machine is gained, privileges must be exploited so the hacker can execute their goal, which generally requires root privileges, to access parts of the system and commands that they should not be able to.

Examples of privilege escalation:
-   Cracking password hashes found on the target
-   Finding a vulnerable service or version of a service which will allow you to escalate privilege THROUGH the service
-   Password spraying of previously discovered credentials (password re-use)
-   Using default credentials
-   Finding secret keys or SSH keys stored on a device which will allow pivoting to another machine
-   Running scripts or commands to enumerate system settings like `ifconfig` to find network settings, or the command `find / -perm \-4000 -type f 2>/dev/null` to see if the user has access to any commands they can run as root

## Covering Tracks
While not required in most professional hacking scenarios, this is still a part of the general methodology. In a professional scenario, the penetration tester should stop immediately when they have escalated privileges, therefore the hacker won't need to cover their tracks because the test was planned and consensual. Often, however, the pen-tester will need to assist the IT administrator in fixing the vulnerability, so it is important to keep detailed notes of your actions. 

## Reporting
This phase involves outlining everything you have found in a report. It often includes the vulnerabilities, the criticality of the finding, a description of how it was found, and recommendations for patching it. 

[Example report](https://github.com/hmaverickadams/TCM-Security-Sample-Pentest-Report) by Heath Adams
