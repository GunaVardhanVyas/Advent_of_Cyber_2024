# Day 14[Certificate_Mismanagement]: Even if we are horribly mismanaged, there'll be no sad faces on SOC-mas!

## Story :
Mayor has been using self-signed cetificate website to spy on the GiftScheduler and the wares of the warewille.

## Learning Objectives : 
- Self-signed certificates
- Man-in-the-middle attacks
- Using Burp Suite proxy to intercept traffic

## Process Key Steps and Points :
- A certificate is comprised of several key components: 
  - A public key, which is used to encrypt data and is accessible to anyone.
  - A private key, kept secret by the website or server, used to decrypt the data.
  - Metadata that provides details about the certificate holder, including information about the Certificate Authority, the website's identity, and the certificate's validity.
- Browsers generally do not trust self-signed certificates because there is no third-party verification. The browser has no way of knowing if the certificate is authentic or if it’s being used for malicious purposes (like a man-in-the-middle attack).
- Trusted CA certificates, on the other hand, are verified by a CA, which acts as a trusted third party to confirm the website’s identity.
 

## Questions, Hints and Answers :
1. What is the name of the CA that has signed the Gift Scheduler certificate?
  - Hint : Read the Certificate when the browser warns you about the risks.
  - ![certi](/Screenshots/D14Q1.png)
  - Ans : `THM`
2. Look inside the POST requests in the HTTP history. What is the password for the snowballelf account?
   - Hint : Go through some of the packets captured.
   - ![snowballelf](/Screenshots/D14Q2.png)
   - Ans : `c4rrotn0s3`
3. Use the credentials for any of the elves to authenticate to the Gift Scheduler website. What is the flag shown on the elves’ scheduling page?
   - Hint : Logout and log back in using any of the elves' creds.
   - ![elf_falg](/Screenshots/D14Q3.png)
   - Ans : `THM{AoC-3lf0nth3Sh3lf}`
4. What is the password for Marta May Ware’s account?
   - Hint : Find mayware's packet.
   - ![marta](/Screenshots/D14Q4.png)
   - Ans : `H0llyJ0llySOCMAS!`
5. Mayor Malware finally succeeded in his evil intent: with Marta May Ware’s username and password, he can finally access the administrative console for the Gift Scheduler. G-Day is cancelled! What is the flag shown on the admin page?
   - Hint : Login as marta mayware and check dashboard.
   - ![flag](/Screenshots/D14Q5.png)
   - Ans : `THM{AoC-h0wt0ru1nG1ftD4y}`
