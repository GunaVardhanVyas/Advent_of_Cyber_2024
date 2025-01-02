# Day 02[Log_Analysis]: One man's false positive is another man's potpourri!

## Story :
Help the awesome Wareville’s SOC team analyse the alerts to determine whether the rumour is true—that Mayor Malware is instigating chaos within the town.

## Learning Objectives : 
- Learn about True Positive and False positives
- Leanr Elastic Tool
- Understand how logs are collected and stored

*Not updated with screenshots and process!*

## Questions, Hints and Answers :
1. What is the name of the account causing all the failed login attempts?
   - Ans : `service_admin`
2. How many failed logon attempts were observed?
   - Ans : `6791`
3. What is the IP address of Glitch?
   - Ans : `10.0.255.1`
4. When did Glitch successfully logon to ADM-01? Format: MMM D, YYYY HH:MM:SS.SSS
   - Ans : `Dec 1, 2024 08:54:39.000`
5. What is the decoded command executed by Glitch to fix the systems of Wareville?
   - Ans : `Install-WindowsUpdate -AcceptAll -AutoReboot`