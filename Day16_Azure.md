# Day 16[Azure]: The Wareville's Key Vault grew three sizes that day!

## Story :
McSkidy finds an intrusion in their Azure tenant, herself and Glitch sit down to discuss and find out the vulnerability that was exploited.

## Learning Objectives : 
- Learn about Azure, what it is and why it is used.
- Learn about Azure services like Azure Key Vault and Microsoft Entra ID.
- Learn how to interact with an Azure tenant using Azure Cloud Shell.

## Abbreviations and Applications :
- [Azure](https://learn.microsoft.com/en-us/azure/?product=popular) : Azure is the cloud computing platform developed by Microsoft.

## Process Key Steps and Points :
- Azure Key Vault:
    Azure Key Vault is an Azure service that allows users to securely store and access secrets. These secrets can be anything from API Keys, certificates, passwords, cryptographic keys, and more.
- Microsoft Entra ID:
    Entra ID is an identity and access management (IAM) service.
  
## Tools and Commands Used :
- `az login -u EMAIL -p PASSWORD` : way-to login
- `az ad signed-in-user show` : show account details of logged-in user
- `az ad user list` : List all users in the tenant
- `az ad user list --filter "startsWith('wvusr-', displayName)"` : some flags for the above command.
- `az ad group list` : list all groups in the tenant
- `az account clear` : logout
- `az role assignment list --assignee REPLACE_WITH_SECRET_RECOVERY_GROUP_ID --all` : check roles available to the group
- `az keyvault secret list --vault-name warevillesecrets` : On having proper access, we can read the vault
- 

## Questions, Hints and Answers :
1. What is the password for backupware that was leaked? 
   - Hint : stored in a different flag seen in `az ad user list --filter "startsWith('wvusr-', displayName)"`
   - ![password](/Screenshots/D16Q1.png)
   - Ans : `R3c0v3r_s3cr3ts!`
2. What is the group ID of the Secret Recovery Group? 
   - Hint : `az ad group list`
   - ![groupid](/Screenshots/D16Q2.png)
   - Ans : `7d96660a-02e1-4112-9515-1762d0cb66b7`
3. What is the name of the vault secret? 
   - Hint : Use `az keyvalut secret list`
   - ![secret](/Screenshots/D16Q3.png)
   - Ans : `aoc2024`
4. What are the contents of the secret stored in the vault? 
   - Hint : check value parameter.
   - ![value_secret](/Screenshots/D16Q4.png)
   - Ans : `WhereIsMyMind1999`
