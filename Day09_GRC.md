# Day 09[GRC]: Nine o' clock, make GRC fun, tell no one.

## Story :
McSkidy and Glitch are seeking a third-party eDiscovery company to process forensic data for their investigation. To make an informed decision, they must conduct a risk assessment on three shortlisted companies. Each company was asked to complete a questionnaire, which will serve as the basis for the risk evaluation process.

## Learning Objectives : 
- Learn about GRC
- Learn different methods to do risk assesment.


## Abbreviations and Applications :
- [GRC](https://aws.amazon.com/what-is/grc/) : Governance, Risk, Compliance.
- [CVSS](https://www.first.org/cvss/) : Common Vulnerability Scoring System, for calculating impact of risks.
- [DREAD](https://learn.microsoft.com/en-us/windows-hardware/drivers/driversecurity/threat-modeling-for-drivers) : A system used by microsoft to assess risk to computer security threats.

## Process Key Steps and Points :
1. **Identification of Risks**
   - An unpatched web server.
   - A high-privileged user account without proper security controls.
   - A third-party vendor who might be infected by a malware connecting to the organisation's network.
   - A system for which support has ended by the vendor and it is still in production.
2. **Assigning Likelihood to each Risk**
   1. Improbable: So unlikely that it might never happen.
   2. Remote: Very unlikely to happen, but still, there is a possibility.
   3. Occasional: Likely to happen once/sometime.
   4. Probable: Likely to happen several times.
   5. Frequent: Likely to happen often and regularly.
3. **Assigning Impact to each Risk**
   1. Informational: Very low impact, almost non-existent.
   2. Low: Impacting a limited part of one area of the organisation's operations, with little to no revenue loss.
   3. Medium: Impacting one part of the organisation's operations completely, with major revenue loss.
   4. High: Impacting several parts of the organisation's operations, causing significant revenue loss
   5. Critical: Posing an existential threat to the organisation.
4. **Risk Ownership**

## Questions, Hints and Answers :
1. What does GRC stand for?
   - Ans : `Governance, Risk,and Compliance`
2. What is the flag you receive after performing the risk assessment?
   - Hint : Just keep playing with the risks, all give the same risk value
   - ![Riskflag](/Screenshots/D9.png)
