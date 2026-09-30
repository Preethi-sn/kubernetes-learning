## OCP - Network

Network configuration of all the resources are configured. CIDR range of service,pod everything is declared here.

      oc get network/cluster -o yaml

Pod-IP - Pod Ip's are used to interact with each other. Using pod ip one pod can able to communicate with another pod. We can't use it to access the application use the pod ip will get changed whenever new pods gets spinned up.

If pods are in same cluster, one pod can interact with other no matter on same project/different project and same/different node. Just it should be in same cluster.

```
 Login to the project: oc new-project or oc project  
 
 deploy app: oc new-app --name=<appname> --image=<image-url>
 
 get the pod info with its name and ip: oc get pod -o wide
 
 login to the pod with its name : oc rsh <podname>
 
 access the application which get deployed on same pod/different pod with curl command
 
 curl http://<app-ip>:<app-port>
```

## Services:

If we create any service for application, it will get created with the type of cluster IP. Which means we can access the application only within the cluster by logging to the node/workernode and curl with service IP and port name

Each time when we access the application , we are getting response from different pod as we have multiple relicas.

<img width="1527" height="795" alt="image" src="https://github.com/user-attachments/assets/8ca1d0db-acd3-40c2-a099-d75725b0610b" />


To login to the node: #oc debug nodes/master01


As an Engineer, we always give the service IP to the client to access the application. Service IP is a static IP and it will never get changed.

Service will identify its pod using labels and selectors. In pod, we declare it as "Labels" and in services, we declare it as "Selectors".

If the label and selector mismatched, it will not be able to communicate.

<img width="1347" height="227" alt="image" src="https://github.com/user-attachments/assets/00f6d67e-a1ca-4c08-af15-5896284cb5ef" />

<img width="1267" height="140" alt="image" src="https://github.com/user-attachments/assets/a5fe5627-5e14-4de4-888a-77780f3814eb" />


## Route

There are 2 types of routes 1) Insecure route 2) Secure route

Application domain names are declared. route base domain name will come from dns pod and its a default pod

oc get dns/cluster-o yaml

To get the route details

oc get routes.routeopenshift.io

### Insecure Route:

To create insecure route:

Method 1:

      #oc get svc
      #oc expose svc <service-name>

<img width="1537" height="287" alt="image" src="https://github.com/user-attachments/assets/0b02fba7-b8fb-4fc9-9d4c-2578a8418cd2" />


#<service-name>-projectname.app.clusterdomain  --> **Route default format**

<img width="1136" height="122" alt="image" src="https://github.com/user-attachments/assets/9c31f8fb-924d-49e4-b34f-6feffb655ccd" />

Method2:

We can also create custom route name on our own as below but the domain name should not be changes :- <custome route name>.apps.ocp4.example.com shouldn't be changed.

oc expose service php-insecure  --hostname=php-insecure.apps.ocp4.example.com

<img width="1502" height="352" alt="image" src="https://github.com/user-attachments/assets/cc73911d-92c1-47d8-93d0-d6d9d13c4bff" />
















