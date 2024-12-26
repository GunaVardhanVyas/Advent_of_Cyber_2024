# Day 5[XXE]: SOC-mas XX-what-ee?

## Story:
The town of Wareville has a new Christmas wish-sharing platform, built by a Soft-Ware and the town's developers. However, the team rushed to meet the deadline and overlooked thorough security testing. Now, it's crucial to ensure the platform is secure and free of vulnerabilities to protect the townspeople's information. Let us explore the vulnerabilities and possibilities for exploitation.

## Learning Objectives:
- Understand the basic concepts related to XMLXML handling data like a file drawer.
- Explore XML External Entity (XXE) and its components
- Learn how to exploit the vulnerability
- Understand remediation measures

## Abbreviations and Applications:
- [XML](https://www.w3schools.com/xml/) : Extensible Markup Language.
- [DTD](https://www.ibm.com/docs/en/dmrt/9.5?topic=dtds-document-type-definitions-overview) : Document Type Definition.
- [XXE](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_(XXE)_Processing) : XML External Entity
- [Burp SUite](https://www.geeksforgeeks.org/what-is-burp-suite/) : Burp Suite is an integrated platform for performing security testing of web applications.

## Process Key Points:
- Application Flow: Users browse products, add to wishlist, view cart, and proceed to checkout, entering name and address.
- Checkout Page: Users complete checkout, and their wish is saved with a unique identifier.
- Intercepting Requests: Burp Suite is used to intercept and manipulate web traffic for exploitation.
- Burp Suite Initialization: Launch Burp Suite, click “Start Burp” on the welcome screen, and familiarize yourself with the main interface.
- Browser Configuration: Enable Burp Suite’s browser to run without a sandbox in the “Settings” tab under the “Tools” section.
- Intercepting Requests: Open the pre-configured Burp Suite browser, navigate to “http://MACHINE_IP”, and observe intercepted requests in the “Proxy->HTTP history” tab. **Dont forget to turn off Interceptor before recording HTTP**
- Vulnerability: The application allows external entity loading in XML parsing, potentially exposing sensitive files or enabling unintended server requests.
- Impact: Attackers can exploit this vulnerability by injecting malicious XML data to access sensitive information or perform unauthorized actions.
- Exploitation: Crafting an XML payload with external entity references, such as file paths or remote URLs, can trigger the vulnerability.
- Vulnerability Exploitation: Repeatedly sending a modified HTTP POST request with a malicious XML payload containing an external entity reference to /etc/hosts.
- Vulnerability Impact: Allows access to sensitive information, such as the wishes placed by the townspeople, by exploiting the XXE vulnerability in the wishlist.php endpoint.
- Vulnerability Identification: Found an XXE vulnerability in the wishlist.php endpoint by sending a request with a malicious XML payload containing an external entity reference to /etc/hosts.
- Vulnerability Exploitation: Leveraged a vulnerability to read the contents of each wishes page, demonstrating the flaw’s extent.
- Payload Construction: Built a payload to read wishes by guessing the absolute path of the file, starting with /var/www/html/wishes/wish_1.txt.
- Impact and Mitigation: Proved the vulnerability’s potential impact by reading all wishes, leading to prompt coordination with developers for mitigation.
- Vulnerability Mitigation: Disable external entity loading in the XML parser and validate/sanitize user input.
- Vulnerability Discovery: McSkidy found a vulnerable code pushed after Software’s team in the CHANGELOG file.
- Suspected Involvement: McSkidy suspected the Mayor’s involvement due to the Mayor’s suspicion and McSkidy’s theories.

## Questions and Hints : 
1. What is the flag discovered after navigating through the wishes?
    - Hint : Wish 17
    - ![Wish_17_flag](/Screenshots/D5Q1.png)
    - Ans : THM{Brut3f0rc1n6_mY_w4y}
2. What is the flag seen on the possible proof of sabotage?
    - Hint : Just browse for IP_addr/CHANGELOG
    - ![Changelog_Flag](/Screenshots/D5Q2.png)
    - Ans : THM{m4y0r_m4lw4r3_b4ckd00rs}