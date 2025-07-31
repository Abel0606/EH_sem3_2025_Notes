#  Assignment 18:Discover Hidden Directories
**Name**: Abel George
**Date**: July 31, 2025
--
## Methodology
Used the gobuster tool on kali linux to discover hidden directories on a web server using Directory enumeration
The purpose of this assignment was to find hidden folders on a website that are not linked from the main page.
By performing reconaissance using this method we might be able to discover sesnitive files or data that shouldnt be public.
Before scanning I had to install gobuster using the following commands:
1)sudo apt update
2)sudo apt install gobuster -y
I performed a scan on the website http://testphp.vulnweb.com using the following command:gobuster dir -u http://testphp.vulnweb.com -w /usr/share/wordlists/dirb/common.txt
<img width="1920" height="936" alt="image" src="https://github.com/user-attachments/assets/27275273-6cb3-46f7-97af-c325a17690c4" />
As you can see,a total of 6 hidden directories were found.Let us go through them one by one;
## 1)/admin/
Under this directory,an admin panel is found although the access to the login page is secured attackers can try to bruteforce credentials.
It also consists of a publically accesible file named "create.sql"-which contains some kind of SQL code
"create.sql" includes  table definitions for databases,which risks revealing database structure, table names, fields—enabling SQL injection or data exfiltration.
## 2)/CVS/
Under this directory,the link takes us to a page containing downloadable files for "Entries" and "Entries.log"
This risks exposure of file paths and code base details.
## 3)/secured/
This directory with sensitive naming implies restricted content.It likely contains backup data and sensitive scripts
Although the link takes us to a blank link a skilled attacker can access and leak internal files,credentials etc
## 4)/vendor/
This directory consists of a link "installed.json" which consists of the following details and more
At the bottom of the screenshot we can see names,email Id's and logs of what people have uploaded
Attackers can identify outdated components and known vulnerabilities for targeted exploits.
## 5)/pictures/
This directory just looks like any other pictures directory with a lot of photos but at the bottom we find 3 major findings
1)A file named "credentials.txt" which contains a username and password
<img width="1920" height="936" alt="image" src="https://github.com/user-attachments/assets/e4bba331-3b63-4936-8144-36c79e953720" />
We know the risk of this as just using reconaissance technique a hacker was able to find the username and password to user.
2)A file named "ipaddresses.txt" which contains the following IP address: 192.168.0.26
Using this an attacker can do infrastrcuture mapping,internal targeting
3)A file named "wp-config.bak" which is a backup copy of a wordpress file which contains DB name,DB username and password
Which an attacker can use to access unauthorized content
