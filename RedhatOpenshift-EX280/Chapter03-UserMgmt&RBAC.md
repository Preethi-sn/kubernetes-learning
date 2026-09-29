**Chapter:03 - User Management**

#oc get identity
#oc whoami -t
To get the pod details of another project(namespace) // -n -> namespace , openshift-authentication -> project name
whenever user gets created in openshift cluster, those details are maintained in oauth-pod under "openshift-authentication"
 namespace. 
**#oc get pod -n openshift-authentication**
 <img width="1355" height="111" alt="image" src="https://github.com/user-attachments/assets/36542432-f2d4-4001-8ac4-3e607b2a332f" />
**oc get oauth cluster -o yaml**
