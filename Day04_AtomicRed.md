# Day 4[Atomic Red Team] : I'm not a hero, I'm just a man with a plan.

## Story:
- GLitch, the towns talented security SOC-researcher decided to revamp the town's security posture. He started by implementing a protective firewall, patching vulnerabilities, and accessing endpoints to patch for security vulnerabilities. As he worked tirelessly, he left "breadcrumbs," small traces of his activity.
- But the SOC team, not knowing the Glitch's true intentions, was suspicious of his actions. They started monitoring his activity, and when they saw the breadcrumbs, they were alarmed. They knew that the Glitch was up to something, but they didn't know what.

## Learning objectives:
- Learn how to identify malicious techniques using the MITRE ATT&CK framework.
- Learn about how to use Atomic Red Team tests to conduct attack simulations.
- Understand how to create alerting and detection rules from the attack tests.

## Abbreviations:
- MITRE ATT&CK: MITRE Adversarial Tactics, Techniques, and Common Knowledge
- Atomic Red Team: A toolset for testing your security posture

## Learning resources:
- [Atomic Red Team](https://atomicredteam.io/)
- [MITRE ATT&CK](https://attack.mitre.org/)
- [Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)

## QUESTIONS : 
1. What was the flag found in the .txt file that is found in the same directory as the PhishingAttachment.xslm artefact?
   - Hint : ![file_dir](/Screenshots/D4Q1.png)
   - Ans : `THM{GlitchTestingForSpearphishing}`
2. What ATT&CK technique ID would be our point of interest? 
   - Hint : ![attackid](/Screenshots/D4Q3.png)
   - Ans : `T1059`
3. What ATT&CK subtechnique ID focuses on the Windows Command Shell? 
   - Ans : `T1059.003`
4. What is the name of the Atomic Test to be simulated? 
   - Hint : ![](/Screenshots/D4Q4.png)
   - Ans : `Simulate BlackByte Ransomware Print Bombing`
5. What is the name of the file used in the test? 
   - Hint : ![](/Screenshots/D4Q5.png)
   - Ans : `Wareville_Ransomware.txt`
6. What is the flag found from this Atomic Test? 
   - Hint : ![flag2](/Screenshots/D4Q6.png)
   - Ans : `THM{R2xpdGNoIGlzIG5vdCB0aGUgZW5lbXk=}`