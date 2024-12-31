# Day 23[Hash_Cracking]: You wanna know what happens to your hashes?

## Story :
The Mayor has been operating a lot, glitch is curious on where from is he getting the funds to do so. So he went to do physical reconnaisance and obtained mayors old tablet which he had thrown away. Desoite its broken condition, it works and glitch recovers a password protected file.

## Learning Objectives : 
- Hash functions and hash values
- Saving hashed passwords
- Cracking hashes
- Finding the password of a password-protected document

## Abbreviations and Applications :
- [SHA256](https://www.simplilearn.com/tutorials/cyber-security-tutorial/sha-256-algorithm) : Secure Hashing Algorithm, with digest value always being 256 bits.
- [MD5](https://www.simplilearn.com/tutorials/cyber-security-tutorial/md5-algorithm) : Message Digest 5 (MD5) is a cryptographic hash function that takes any input and produces a 128-bit hexadecimal number.
- digest : output of a hashing function.
- [John the Ripper](https://www.openwall.com/john/) : John the Ripper is a free and open-source password-cracking tool. It can crack passwords stored in various formats, including hashes, passwords, and encrypted private keys.

## Process Key Steps and Points :
- Data in Transit and Data at rest.
- Use john. john jumbo package has all tools name `*2john*`, out of which we can use `pdf2john.pl`. Others include `jpg2john.py`.

## Tools and Commands Used :
- `john --format=raw-sha256 --wordlist=/usr/share/wordlists/rockyou.txt hash1.txt` : john the ripper tool
- `--rules=wordlist` : checks all possibilities of symbols being substitutes to letters such as i,! and a,@ and so on.
- `john --format=raw-sha256 --show hash1.txt` : All cracked passwords are stored once cracked.
- `pdftotxt private.pdf -upw password` : To convert pdf to text, even password protected pdfs.

## Questions, Hints and Answers :
1. Crack the hash value stored in hash1.txt. What was the password?
   - Hint : Use the `--show` option in `john`.
   - ![hash_pass](/Screenshots/D23Q1.png)
   - Ans : `fluffycat12`
2. What is the flag at the top of the private.pdf file?
   - Hint : use `pdftotxt private.pdf -upw password` and the password can be cracked from `john`.
   - ![password](/Screenshots/D23Q2a.png)
   - Password : `M4y0rM41w4r3`
   - ![flag](/Screenshots/D23Q2.png)
   - Ans : `THM{do_not_GET_CAUGHT}`