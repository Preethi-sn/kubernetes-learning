# Openshift Networking basics

## OCP - Network

Pod-IP - Pod Ip's are used to interact with each other. Using pod ip one pod can able to communicate with another pod. We can't use it to access the application use the pod ip will get changed whenever new pods gets spinned up.

If pods are in same cluster, one pod can interact with other no matter on same project/different project and same/different node. Just it should be in same cluster.

 Login to the project: oc new-project or oc project  
 
 deploy app: oc new-app --name=<appname> --image=<image-url>
 
 get the pod info with its name and ip: oc get pod -o wide
 
 login to the pod with its name : oc rsh <podname>
 
 access the application which get deployed on same pod/different pod with curl command
 
 curl http://<app-ip>:<app-port>
