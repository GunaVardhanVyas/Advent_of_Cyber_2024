# Day 20[Taffic_Analysis]: If you utter so much as one packet...

## Story :
Glitch captures traffic with delicate ease, and the PCAP file of the latest victim Marta Mayware's system was captured and sent to McSkidy for analysis.

## Learning Objectives : 
- Investigate network traffic using Wireshark
- Identify indicators of compromise (IOCs) in captured network traffic
- Understand how C2 servers operate and communicate with compromised systems

## Abbreviations and Applications :
- [PCAP](https://linux.die.net/man/3/pcap) : Packet capture ,is a networking practice involving the interception of data packets travelling over a network.
- [IOC](https://www.crowdstrike.com/en-us/cybersecurity-101/threat-intelligence/indicators-of-compromise-ioc/) : Indicator of Compromise.
- [Wireshark](https://www.wireshark.org/about.html) : Wireshark is the world's foremost network protocol analyzer. 
- [C2](https://www.splunk.com/en_us/blog/learn/c2-command-and-control.html) : Command and Control (C2) Infrastructure are a set of programs used to communicate with a victim machine.
- [AES]() : The Advanced Encryption Standard (AES) is a symmetric block encryption algorithm. It can use cryptographic keys of sizes 128, 192, and 256 bits.
- 
## Process Key Steps and Points :
- Whenever a machine is compromised, the command and control server (C2) drops its secret agent (payload) into the target machine.
- Then the attakcer could do any one of the following by sending the compromised system a command based on his requiements, capabilities and intentions.
  1. Getting System Information
  2. Executing Commands
  3. Downloading and executing Payloads
  4. Exfiltrating Data
- Following Streams we find out the interactions between payload and the C2 Server.

## Tools and Commands Used :
- `ip.src == ip_addr` : filters all packets sourcing from ip_addr.
- `tcp eq #num` : to follow a communication stream. Also can do `Follow->HTTP Stream`.

## Questions, Hints and Answers :
1. What was the first message the payload sent to Mayor Malware’s C2?
   - Hint : Just follow the streams in the room
   - ![payload_message](/Screenshots/D20Q12.png)
   - Ans : `I am in Mayor!`
2. What was the IP address of the C2 server? 
   - Hint : Check the previous stream itself.
   - Ans : `10.10.123.224`
3. What was the command sent by the C2 server to the target machine? 
   - Hint : Check Stream 2.
   - ![commC2](/Screenshots/D20Q3.png)
   - Ans : `whoami`
4. What was the filename of the critical file exfiltrated by the C2 server? 
   - Hint : Check Stream 3.
   - ![exfil](/Screenshots/D20Q4.png)
   - Ans : `credentials.txt`
5. What secret message was sent back to the C2 in an encrypted format through beacons?
   - Hint : Check Stream 4 for encrypted text and key from stream 3 and use cyberchef to decode the AES ECB.
   - ![encrypt_text](/Screenshots/D20Q5a.png)
   - ![decrpt_text](/Screenshots/D20Q5.png)
   - Ans : `THM_Secret_101` 

