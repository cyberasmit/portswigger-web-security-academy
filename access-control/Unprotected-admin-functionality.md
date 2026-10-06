# Lab: Unprotected admin functionality

## Vulnerability
unprotected admin functionality
## Level 
apprentice
## Lab URL 
"https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/access-control-apprentice/access-control/lab-unprotected-admin-functionality#"
---
## Objective 
Delete an user 'carlos' by accessing the administrative panel.
## Analysis & Discovery
1.Accessed the lab and opened the inspection mode first and found nothing there.
2.Decided to check the "robots.txt".
3.found something interesting there 'User-agent: *.
                                     Disallow: /administrator-panel'.
## Exploitation steps
1. see "/administrator-panel".
2. replace "url/robots.txt" with "url/administrator-panel".
3. Now you have access to the administrator panel , delete the user 'carlos' and your lab is complete.

