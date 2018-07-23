
## Introduction 
The documetnation contains for DevOps take home. 

## Output

 - Front-end application can be found:  
http://nltapp0001.azurewebsites.net/  
 - We can see new entries from related DB as well:    
![](./images/DevOps01.png)   


## Infrastructre underneath 

- Two App Services on one App Service Plan

-  Backend is properly communicating with DB showing entries, e.g.:  
![](./images/DevOps02.png)   
-  Azure SQL is protected by Firewall with whitelistng only IPs of back-end App Service:  
![](./images/DevOps03.png)   

## Future improvements  

 - For strenghten Backend API from external we could use: 
  - When keeping the current App Service architecture. Then implement Service to Service authentication (with e.g. auth tokens)  
  That will respond with 401 when reaching particular endpoint when not authenticated (but not 403 that doesn't exist).  

  - Change infrasturcture architecutre to Service Fabric with Application Gateway. For external, publicly exposed endpont so front-end would be dedicated API rules in the Application Gateway (under Rules aka ReverseProxy). Further for internal use only there will be the back-end service with /api/incidents. Then rest of incoming requests blocked under HTTP Settings.  
  Diagram can be prepared upon request.  
  To accomplish such scenario my current Azure subscription's limit will be exahasuted in 4 days. 

  

  - Azure Service Environments with internal load balancer
  My Azure subscription will be eahasuted in 2 working days.       

- To further more protect SQL from outside: 
 - With Service Fabric or ASE approach. Using VNET endpoint peering to the SQL Server - to whitelist the only VNET
 - When need to totaly not having any external name avalialbe. Then we need to have dedicated VM with MS SQL installed with only Private IP. Then back-end would be in the same network and reaching such IP.  

 ## IaaC / DevOps pipeline   
 
The solution has been prepared in Vistual Studio Team Services with levaraging ARM and PowerShell scripts. 
 - Using Build for building back-end App  
 - Using Relase to:
  - Publish back-end App to App Service from Build's artefact
  - Publish fron-end to App Service
Further e.g. screenshots are available upon request.  