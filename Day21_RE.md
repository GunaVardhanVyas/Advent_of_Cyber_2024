# Day 21[Reverse_Engineering]: HELP ME!...I'm REVERSE ENGINEERING!

## Story :
Glitch had built a file-sharing web application, and now there was an unknown binary file compiled with .NET in the backend of the application. This triggered an alert on McSkidy's dashboard. Let us try to figure out what this file is.

## Learning Objectives : 
- Understanding the structure of a binary file 
- The difference between Disassembly vs Decompiling
- Familiarity with multi-stage binaries
- Practically reversing a  multi-stage binary

## Abbreviations and Applications :
- [RE](https://www.eccouncil.org/cybersecurity-exchange/ethical-hacking/malware-reverse-engineering/) : Reverse Engineering, is the process of breaking something down to understand its function.
- [Ghidra](https://ghidra-sre.org/) : Ghidra is a software reverse engineering (SRE) framework created and maintained by the National Security Agency Research Directorate. 
- [ILSpy](https://github.com/icsharpcode/ILSpy) : .NET Decompiler
- [PE](https://learn.microsoft.com/en-us/windows/win32/debug/pe-format) : Portable Executable.

## Process Key Steps and Points :
- All binaries have:
  - A code section: This section contains the instructions that the CPU will execute
  - A data section: This section contains information such as variables, resources (images, other data), etc
  - Import/Export tables: These tables reference additional libraries used (imported) or exported by the binary. Binaries often rely on libraries to perform functions. For example, interacting with the Windows API to manipulate files
- Reverse Engineering mainly composed of two techniques, deassembling and decompiling.
  - Disassembling a binary shows the low-level machine instructions the binary will perform.
  - Decompiling converts the binary into its high-level code, such as C++, C#, etc., making it easier to read. But it loses information often such as variable names.
- Theres usually multiple staged binaried for exploitation, which usually follow the following process:
  - Stage 1 - Dropper: This binary is usually a lightweight, basic binary responsible for actions such as enumerating the operating system to see if the payload will work. Once certain conditions are verified, the binary will download the second - much more malicious - binary from the attacker's infrastructure.
  - Stage 2 - Payload: This binary is the "meat and bones" of the attack. For example, in the event of ransomware, this payload will encrypt and exfiltrate the data.

## Questions, Hints and Answers :
1. What is the function name that downloads and executes files in the WarevilleApp.exe? 
   - Hint : Just read and check the functions. Hint in Q3 screenshot.
   - Ans : `DownloadAndExecuteFile`
2. Once you execute the WarevilleApp.exe, it downloads another binary to the Downloads folder. What is the name of the binary?
   - Hint : Just read the logs. Hint in Q3 screenshot.
   - Ans : `explorer.exe`
3. What domain name is the one from where the file is downloaded after running WarevilleApp.exe? 
   - Hint : Check around the same decompiler.
   - ![func](/Screenshots/D21Q123.png)
   - Ans : `mayorc2.thm`
4. The stage 2 binary is executed automatically and creates a zip file comprising the victim's computer data; what is the name of the zip file? 
   - Hint : Do the same process to the `explorer.exe` that was downloaded for stage-2.
   - Ans : `CollectedFiles.zip`
5. What is the name of the C2 server where the stage 2 binary tries to upload files?
   - Hint : Seen in the source codee.
   - ![c2server](/Screenshots/D21Q45.png)
   - Ans : `anonymousc2.thm`
