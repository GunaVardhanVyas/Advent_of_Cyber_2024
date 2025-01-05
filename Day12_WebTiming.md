# Day 12[Web_Timing]: If I can't steal their money, I'll steal their joy!

## Story :
Warevilles banks had huge profits and wanted to publicly announce and have a party. But when they were about to close up they were shocked to see that their work has been upside down and now they were incurring heavy loss. This was the work of mayor and his minions, who have exploited the HTTP/2 workings and made the banks pass even the unauthorised transactions.

## Learning Objecctives : 
- Understand the concept of race condition vulnerabilities
- Identify the gaps introduced by HTTP2
- Exploit race conditions in a controlled environment
- Learn how to fix the race

## Abbreviations and Applications :
- [HTTP/2](https://http2.github.io/) : The major update to HTTP/1.1 (Hyper Text Transfer Protocol). It is the protocol used for most of the web applications.

## Process Key Steps and Points :
- **Web Timing and Race Conditions :**
  - In its simplest form, a <u>web timing attack</u> means we glean information from a web application by reviewing how long it takes to process our request. By making tiny changes in what we send or how we send it and observing the response time, we can access information we are not authorised to have.
  - <u>Race conditions</u> are a subset of web timing attacks that are even more special. With a race condition attack, we are no longer simply looking to gain access to information but can cause the web application to perform unintended actions on our behalf.
- **Typical Timing Attacks :**
  - **Information Disclosures**
        Leveraging the differences in response delays, a threat actor can uncover information they should not have access to. For example, timing differences can be used to enumerate the usernames of an application, making it easier to stage a password-guessing attack and gain access to accounts.
  - **Race Conditions**
        Race conditions are similar to business logic flaws in that a threat actor can cause the application to perform unintended actions. However, the issue's root cause is how the web application processes requests, making it possible to cause the race condition. For example, if we send the same coupon request several times simultaneously, it might be possible to apply it more than once.

## Questions, Hints and Answers :
>What is the flag value after transferring over $2000 from Glitch's account?
>![flag](/Screenshots/D12.png)
>Ans : `THM{WON_THE_RACE_007}`