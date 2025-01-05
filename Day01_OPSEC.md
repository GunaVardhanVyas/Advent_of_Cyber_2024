# Day 01[OPSEC]: Maybe SOC_mas music, he thought, doesn't come from as store?

/*Could not get proper screenshots, will try adn attatch them for the first 2-3 days*/

## Story :
McSkidy has been looking for any malware that could easily spread at this time of the year. She has come accross a shady website that was publicised for being able to download music in mp3 format from various website. But what happens in the background is that the website downloads two files with similar names, one being the actual song but other one being a powershell executive, executing which gives 

## Learning Objectives : 
- Learn how to investigate malicious link files.
- Learn about OPSEC and OPSEC mistakes.
- Understand how to track and attribute digital identities in cyber investigations.

## Abbreviations and Applications :
- [OPSEC](https://www.fortinet.com/resources/cyberglossary/operational-security) : Operation Security.

## Process Key Steps and Points :
- Youtube to MP3 converters:
  - Malvertising: Many sites contain malicious ads that can exploit vulnerabilities in a user's system, which could lead to infection.
  - Phishing scams: Users can be tricked into providing personal or sensitive information via fake surveys or offers.
  - Bundled malware: Some converters may come with malware, tricking users into unknowingly running it.
- We need to check the type of file and follow it back to check where it was downloaded from and we are directed to a github repo.
- By the mistake of the ware, we find out a comment from the attacker and following that account we can find out the true identity of the attacker.


## Tools and Commands Used :
- `file somg.mp3` : file type 
- `exiftool somg.mp3` : file details

## Questions, Hints and Answers :
1. Looks like the song.mp3 file is not what we expected! Run "exiftool song.mp3" in your terminal to find out the author of the song. Who is the author? 
   - Ans : `Tyler Ramsbey`
2. The malicious PowerShell script sends stolen info to a C2 server. What is the URL of this C2 server?
   - Ans : `http://papash3ll.thm/data`
3. Who is M.M? Maybe his Github profile page would provide clues?
   - Ans : `Mayor Malware`
4. What is the number of commits on the GitHub repo where the issue was raised?
   - Ans : `1`
