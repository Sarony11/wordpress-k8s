## Wordpress in K8S with external database
In this project, we have a wordpress deployment in K8S but configuring an external database instead of a container db with a PV.

### Files
#### wordpress-deployment.yaml
Deploy the wordpress application with a PV for /var/www/html where all the wodpress internal code and data is stored.

#### pv-claim.yaml
A PV claim for the the wordpress-deplomyment.yaml PV.

#### wordpress-clusterip-service.yaml
We create a ClusterIP service for our deployment. This only gives internal access, so we also need an ingress to expose the app to internet.

#### ingress-service.yaml
This ingress translates external access to 80 port to the ClusterIP
Ingress(public_ip:80) --> ClusterIP (internal_ip:80) --> Wordpress (Apache:80) 
*To run this ingress resource, we have to enable ingress-nginx

#### kustomaization.yaml
This file is the one executed by kubectl and creates in a declarative way the Secret needed for the mysql password. Moreover, executes the rest of listed .yaml files.

### How to execute
```
kubectl apply -k .
```
