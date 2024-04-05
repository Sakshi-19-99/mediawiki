# mediawiki
MediaWiki Deployment on Kubernetes using Helm
This repository includes guidelines and config files for setting up MediaWiki on Kubernetes with the help of Helm. 

Pre-requisites
1. Installed Kubernetes
2. Installed Helm
3. Installed Azure CLI

Installation Steps:
Steps to deploy MediaWiki on Kubernetes:
1. Clone the repository
2. Log in to azure account
3. Create resource group and aks cluster
4. Deploy MediaWiki using following commands:
   #Create a Helm Chart for MediaWiki
   helm create mediawiki

   #Modify Values in the created values.yaml file:
   values.yaml

   #Install the Helm chart:
   helm install mediawiki ./mediawiki

5. Monitor Deployment using following command:
   helm install mediawiki ./mediawiki

6.Access MediaWiki:
  http://mediawiki.example.com/

Attached screenshot for reference:
![image](https://github.com/Sakshi-19-99/mediawiki/assets/71216065/81528ced-8582-4f9b-bdb7-b1738c5584f7)



