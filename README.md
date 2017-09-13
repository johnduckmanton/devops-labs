# Working repo for DevOps labs 

Current strawman skeleton layout (not fixed, please change and move stuff!)

"Complete" Node DevOps Lab
 - Part 1 - Creating app & CI
 - Part 2 - Starting CD - IaC & ARM
 - Part 3 - Rest of CD (release) & App Insights


### Thoughts / Discussion Area
- Other platforms? Worth including?
  - .NET Core
  - Python
  - Java 
  - PHP 
  - Full .NET (erggh!)
- "Lite" version?
  - Maybe skip to the VSTS part with a pre created app/src?
  - Remove the IaC component and deploy to existing resources, is this not DevOps-y enough?
- Other labs I've created - how do we include (or superceed?)
  - Node + VSTS deployed via Docker and ACR to Linux Web App  
  https://github.com/benc-uk/azure-node-docker-paas  
  *Similar to the "complete" lab but deploys using Docker and misses out the complex IaC/ARM stuff*
  - .NET Core + VSTS + Docker Machine  
  https://github.com/benc-uk/azure-devops-core-docker  
  *Not looked at this for a while, probably needs a refresh, using Docker Machine seems a bit IaaS-y now we have ACI*