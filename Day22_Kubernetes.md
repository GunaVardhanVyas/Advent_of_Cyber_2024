# Day 22[Kubernetes_DFIR]: It's because I'm kubed, isnt it?

## Story :
Mayor Malware has been very eager to check if he has made the nice in nice or naughty list. So abusing his power he has scheduled a sudden mayor inspection and so the wares had to give him a temp access. But when he checked the next day he was on the top of the naughty list.

## Learning Objectives : 
- Learn about Kubernetes, what it is and why it is used.
- Learn about DFIR, and the challenges that come with DFIR in an ephemeral environment.
- Learn how DFIR can be done in a Kubernetes environment using log analysis.

## Abbreviations and Applications :
- [Kubernetes](https://kubernetes.io/docs/home/) : Kubernetes is a container orchestration system used for automating deployment, scaling and management of applications.
- [DFIR](https://www.ibm.com/think/topics/dfir) : Digital Forensics and Incident Response.

## Process Key Steps and Points :
- In **Kubernetes**, containers run in pods; these pods run on nodes, and a collection of nodes makes up a Kubernetes cluster.
- **DFIR**,
  - **Digital Forensics** aims to collect and analyse digital evidence of an incident.
  - **Incident Response** relies in data analysis to investigate an incident and focuses on "responsive" actions such as threat containment and system recovery.
- `PATCH` method is used to update docker images in a registry.

## Tools and Commands Used :
- `minikube start` : start a cluster.
- `kubectl get pods -n wareville` : verify the cluster status and contents.
- `kubectl exec -n wareville naughty-or-nice -it -- /bin/bash` : Connect to naughty-or-nice pod in wareville cluster.
- `cat /var/log/apache2/access.log` : access Apache2 logs.
- `docker ps` : list docker containers.
- `grep "PATCH"` : pull the logs where image was updated.
- `kubectl get rolebindings -n wareville` : check role bindings
- `kubectl describe rolebinding mayor-user-binding -n wareville` : describe a particular role binding
- `kubectl get secret pull-creds -n wareville -o jsonpath='{.data.\.dockerconfigjson}' | base64 --decode` : get screts.

## Questions, Hints and Answers :
1. What is the name of the webshell that was used by Mayor Malware?
   - Hint :
   - ![name](/Screenshots/D22Q12.png) 
   - Ans : `shelly.php`
2. What file did Mayor Malware read from the pod?
   - Ans : `db.php`
3. What tool did Mayor Malware search for that could be used to create a remote connection from the pod?
   - Ans : `nc`
4. What IP connected to the docker registry that was unexpected?
   - ![IPcon](/Screenshots/D22Q4.png)
   - Ans : `10.10.130.253`
5. At what time is the first connection made from this IP to the docker registry?
   - ![firstCon](/Screenshots/D22Q5.png)
   - Ans : `29/Oct/2024:10:06:33 +0000`
6. At what time is the updated malicious image pushed to the registry?
   - ![imgPATCH](/Screenshots/D22Q6.png)
   - Ans : `29/Oct/2024:12:34:28 +0000`
7. What is the value stored in the "pull-creds" secret?
   - Hint : `kubectl get secret pull-creds -n wareville -o jsonpath='{.data.\.dockerconfigjson}' | base64 --decode`
   - ![pull_creds](/Screenshots/D22Q7.png)
   - Ans : `{"auths":{"http://docker-registry.nicetown.loc:5000":{"username":"mr.nice","password":"Mr.N4ughty","auth":"bXIubmljZTpNci5ONHVnaHR5"}}}`