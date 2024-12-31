# Day 17[Log_Analysis]: He analyzed and analyzed till his analyzer was sore!

## Story :
Someone has disonnected the main server from the Warevilles servers, and the CCTV footage was deleted. The only one who can access the CCTV footage and logs is Byte, Glitch's dog who had been nothing but faithful. Clearly someone is pinning allegations and vexing the hardworking dog.

## Learning Objectives : 
- Learn how to extract custom fields in Splunk
- Learn to create a parser for the custom logs
- Filter and narrow down the search results using Search Processing Language (SPL)
- How to investigate in Splunk

## Abbreviations and Applications :
- [SIEM](https://www.microsoft.com/en-in/security/business/security-101/what-is-siem) : Security Information and Event Management system that is used to aggregate security information in the form of logs, alerts, artifacts and events into a centralized platform that would allow security analysts to perform near real-time analysis during security monitoring.
- [Splunk](https://docs.splunk.com/Documentation) : Splunk is a platform for collecting, storing, and analysing machine data. It provides various tools for analysing data, including search, correlation, and visualisation. It is a powerful tool that organisations of all sizes can use to improve their IT operations and security posture.
- [SPL](https://docs.splunk.com/Splexicon:SPL) : Search Processing Language. A processing language used for searching in Splunk.

## Tools and Commands Used :
- `^(?P<timestamp>\d+\-\d+\-\d+\s+\d+:\d+:\d+)\s+(?P<Event>(Login\s\w+|\w+))\s+(?P<user_id>\d+)?\s?(?P<UserName>\w+)\s+.*?(?P<Session_id>\w+)$` Regex
- `index=cctv_feed | stats count(Event) by UserName`
- `index=cctv_feed *put_Session_id_here* | table _time UserName Event Session_id`
- `index=web_logs clientip="10.11.105.33" | table _time clientip status uri ur_path file`
- `index=cctv_feed *lsr1743nkskt3r722momvhjcs3*`

## Questions, Hints and Answers :
1. Extract all the events from the cctv_feed logs. How many logs were captured associated with the successful login?
   - Hint : Use `index=cctv_feed | stats count by Event`
   - ![sucLog](/Screenshots/D17Q1.png)
   - Ans : `642`
2. What is the Session_id associated with the attacker who deleted the recording?
   - Hint : Use `index=cctv_logs *DELETE*`
   - ![sesID](/Screenshots/D17Q2.png)
   - Ans : `rij5uu4gt204q0d3eb7jj86okt`
3. What is the name of the attacker found in the logs, who deleted the CCTV footage?
   - Hint : Use `index=cctv_feed *lsr1743nkskt3r722momvhjcs3*`
   - ![culprit](/Screenshots/D17Q3.png)
   - Ans : `mmalware`