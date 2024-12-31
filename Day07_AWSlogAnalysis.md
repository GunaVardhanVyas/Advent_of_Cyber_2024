# Day 07[AWS Log Analysis]: Oh, no. I'M SPEAKING IN CLOUDTRAIL!

## Story :
Care4Wares made it their mission that all wares who dont, be provided something to read. So they have gone to the store to buy some books and the distribute them to the wares of Wareville. But while paying, their transaction was declined due to insufficient funds, this shouldn't have happened as Care4Wares had rolled out a digital flyer asking for donations and a lot of the people have donated but these transactions werent showing. On chechking the AWS vault where they had linked their QR on the flier, someone had changed the QR code. Lets find out who was behind this heinous and cruel crime.

## Learning Objectives : 


## Abbreviations and Applications :
- [JQ](https://jqlang.github.io/jq/manual/) : helps us transform and filter that JSON data into meaningful data we can understand and use to gain security insights.
- [AWS](https://aws.amazon.com/what-is-aws/) : Amazon Web Services.
- [IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) : Identity and Access Management, is a web service that helps you securely control access to AWS resources.
- [JSON](https://www.json.org/json-en.html) : Java Script Object Notation, is a lightweight data-interchange format.
- 

## Process Key Steps and Points :
- CloudWatch : AWS CloudWatch is a monitoring and observability platform that gives us greater insight into our AWS environment by monitoring applications at multiple levels. CloudWatch provides functionalities such as the monitoring of system and application metrics and the configuration of alarms on those metrics for the purposes of today's investigation, though we want to focus specifically on CloudWatch logs.
  Log Events: A log event is a single log entry recording an application "event"; these will be timestamped and packaged with log messages and metadata.
  Log Streams: Log streams are a collection of log events from a single source.
  Log Groups: Log groups are a collection of log streams. Log streams are collected into a log group when logically it makes sense, for example, if the same service is running across multiple hosts.
- CloudTrail : to monitor actions in your AWS environment.
    - Always On: CloudTrail is enabled by default for all users
    - JSON-formatted: All event types captured by CloudTrail will be in the CloudTrail JSON format
    - Event History: When users access CloudTrail, they will see an option "Event History", event history is a record of the actions that have taken place in the last 90 days. These records are queryable and can be filtered on attributes such as "resource" type.
    - Trails: The above-mentioned event history can be thought of as the default "trail," included out of the box. However, users can define custom trails to capture specific actions, which is useful if you have bespoke monitoring scenarios you want to capture and store beyond the 90-day event history retention period.
    - Deliverable:  As mentioned, CloudWatch can be used as a single access point for logs generated from various sources; CloudTrail is no different and has an optional feature enabling CloudTrail logs to be delivered to CloudWatch.
- 
## Tools and Commands Used :
- `jq -r '.Records[] | select(.eventSource == "s3.amazonaws.com" and .requestParameters.bucketName=="wareville-care4wares")' cloudtrail_log.json`
- `jq -r '["Event_Time", "Event_Name", "User_Name", "Bucket_Name", "Key", "Source_IP"],(.Records[] | select(.eventSource == "s3.amazonaws.com" and .requestParameters.bucketName=="wareville-care4wares") | [.eventTime, .eventName, .userIdentity.userName // "N/A",.requestParameters.bucketName // "N/A", .requestParameters.key // "N/A", .sourceIPAddress // "N/A"]) | @tsv' cloudtrail_log.json | column -t`
- ``` jq -r '["Event_Time", "Event_Source", "Event_Name", "User_Name", "Source_IP"],(.Records[] | select(.userIdentity.userName == "glitch") | [.eventTime, .eventSource, .eventName, .userIdentity.userName // "N/A", .sourceIPAddress // "N/A"]) | @tsv' cloudtrail_log.json | column -t -s $'\t' ```


## Questions, Hints and Answers :
1. What is the other activity made by the user glitch aside from the ListObject action?
   - Ans : `PutObject`
2. What is the source IP related to the S3 bucket activities of the user glitch?
   - Ans : `53.94.201.69`
3. Based on the eventSource field, what AWS service generates the ConsoleLogin event?
   - Ans : `signin.amazonaws.com`
4. When did the anomalous user trigger the ConsoleLogin event?
   - Ans : `2024-11-28T15:21:54Z`
5. What was the name of the user that was created by the mcskidy user?
   - Ans : `glitch`
6. What type of access was assigned to the anomalous user?
   - Ans : `AdministratorAccess`
7. Which IP does Mayor Malware typically use to log into AWS?
   - Ans : `53.94.201.69`
8. What is McSkidy's actual IP address?
   - Ans : `31.210.15.79`
9. What is the bank account number owned by Mayor Malware?
    - Ans: `2394 6912 7723 1294`
