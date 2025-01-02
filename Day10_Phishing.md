# Day 10[Phishing]: He had a brain full of macros, and had shells in his soul.

## Story: 
Marta May-ware's system was compromised even when she had followed all the procedures. McSkidy and Glitch find out that she had clicked on a macro and the mayor had gotten complete access of her system. Let us run an assesment and improve the security.

## Learning Objectives :
- Understand how phishing attacks work.
- Discover how macros in documents can be used and abused
- Learn how to carry out a phishing attack with a macro

## Abbreviations and Applications :
- [Macros](https://www.digitalguardian.com/blog/what-macro-malware) : is a set of programmed instructions designed to automate repetitive tasks.
- [Metasploit](https://www.metasploit.com/) : It's an essential tool for discovering hidden vulnerabilities using a variety of tools and utilities.

## Process : 
> Key steps for phishing using macros:
> 1. Create a document with a malicious macro
> 2. Start listening for incoming connections on the attacker’s system
> 3. Email the document and wait for the target user to open it
> 4. The target user opens the document and connects to the attacker’s system
> 5. Control the target user’s system

**Key Steps and Points :** 
- Malicious Document Creation: Create a document with a malicious macro using Metasploit Framework.
- Metasploit Configuration: Set payload, exploit module, attacker’s IP address, and listening port.
- Connection Establishment: Listen for incoming connections from the victim’s system.
- Exploit Module: multi/fileformat/office_word_macro.
- Payload: windows/meterpreter/reverse_tcp.
- Exploit Target: Microsoft Office Word on Windows.
- Exploit Creation: The exploit creates a macro-enabled Word document (msf.docm) with a payload embedded in the document’s comments.
- Macro Functionality: The macro automatically executes when the document is opened, decodes the payload from the comments, and then executes it on the target system.
- Payload Execution: The payload is an executable file that connects to the attacker’s system IP address and port.
- Malicious File Conversion: Convert a base64 encoded file back to its original executable format using the base64 command.
- File Behavior Verification: Check the behavior of a file in a sandbox environment using a service like VirusTotal.
- Incoming Connection Handling: Use Metasploit to listen for incoming connections when a target user opens a phishing document.
- Exploit Setup: Using the multi/handler module with payload windows/meterpreter/reverse_tcp, listening on CONNECTION_IP:8888.
- Payload Configuration: LHOST set to CONNECTION_IP and LPORT set to 8888.
- Next Steps: Send the malicious document to the target user using the provided email credentials.
- Exploitation Technique: Typosquatting, using a domain name similar to the target’s to trick them into opening a malicious email attachment.
- Email Attachment: A document disguised as an invoice or receipt, attached to an email sent to the target.
- Exploit Outcome: A reverse shell on the target system, allowing access to files and folders via the command line.

## Question and Hints :
> **What is the flag value inside the flag.txt file that’s located on the Administrator’s desktop?**
>> Hint : go the the exact directory and use cat command, other techniques may or may not work.
>> ![flag_phishing](/Screenshots/D10Q1.png)
>> Ans : THM{PHISHING_CHRISTMAS}