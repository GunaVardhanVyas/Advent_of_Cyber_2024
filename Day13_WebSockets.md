# Day 13[WebSockets]: It came without buffering! It came without lag!

## Story :
Wares are all about security. The Glitch discovers that an app is illegally tracking the cars in Wareville. Not many car thefts in the city warrant such an extreme measure. He reaches out to McSkidy to investigate and identify how the application is tracking them and leaking users' positions.

## Learning Objecctives : 
- Learn about WebSockets and their vulnerabilities.
- Learn how WebSocket Message Manipulation can be done.

## Process Key Steps and Points :
- Web sockets are better for live data and chats as they provide an open connection once authenticated, unlie classic HTTP which has to send requests for each message. There is something known as polling that browser automatically sends requests periodically, but it utilizes more resources than websockets.
- However, WebSockets pose several security risks if not properly managed. Some of the key concerns include:
    * **Lack of built-in authentication** and authorization mechanisms, making it easier for attackers to gain unauthorized access to sensitive data.
    * Vulnerability to **message tampering**, which can allow attackers to intercept and alter messages, potentially injecting malicious commands or altering data.
    * **Cross-Site WebSocket Hijacking (CSWSH)**, where an attacker tricks a user's browser into establishing a WebSocket connection with a malicious server, potentially allowing the attacker to access sensitive data or hijack the connection.
    * **Denial of Service (DoS)** attacks, where an attacker floods the server with a large volume of messages, potentially causing it to slow down or crash.
- A malicious actor could exploit WebSocket vulnerabilities to carry out unauthorized actions, such as:
    * Impersonating users to make purchases, transfer funds, or modify account settings
    * Manipulating transaction amounts or routing payments to their own account
    * Gaining access to admin controls, changing user data, or viewing sensitive information
    * Feeding bad data into the system, leading to data corruption
    * Disrupting shared workflows or tools by changing data in real-time
    * Overwhelming the server with bad requests, causing it to slow down or crash, resulting in downtime for users and businesses.

## Questions, Hints and Answers :
1. What is the value of Flag1?
   - Hint : Follow the steps and change userid from 5 to 8.
   - ![flag1](/Screenshots/D13Q1.png)
   - Ans : `THM{dude_where_is_my_car}`
2. What is the value of Flag2?
   - Hint : Try sending a message, intercept it and change its userid to 8.
   - ![flag2](/Screenshots/D13Q2.png)
   - Ans : `THM{my_name_is_malware._mayor_malware}`

