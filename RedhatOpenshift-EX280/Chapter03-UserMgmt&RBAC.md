# chapter:03 - User Management
1. Initiate lab: To make the cluster ready for the excerise
2. login with admini,developer,kubadmin
oc login -u kubeadmin -p yyUai-QPoXs-xBYSN-UJITn https://api.ocp4.example.com:6443
3. #oc new-project user-demo -> create new project
4. #oc whoami -t
##Step:1 - Create user using htpasswd tool
       To create user, we have to use htpasswd tool. check if its installed (#htpasswd). If not, install it.
       **sudo yum install httpd-tools -y**
7. Create directory **#mkdir user-details** directory name can be anything.
8. Create user, **#htpasswd -c -b -B user-details/users.config <username> <password>**
           a.**-c** - create users.config file (use this -c option when we are creating the user.config file first time. from next time dont use c as it will create new config file and delete the existing file and create new and old username will also get removed)
          b.**-b** - is to inject the user password in the file along with username
          c.**-B** - to secure the password safely in users.config file.
<img width="1521" height="410" alt="image" src="https://github.com/user-attachments/assets/fd9e4430-7975-447f-ba0c-3b77e37412e6" />
                              **step:2 - Convert the user config into secrets and inject the secret in openshift-config namespace**
1. To get the list of existing secrets in openshift-config namespace.
   **#oc get secrets -n openshift-config**
2. To create secret for user config file
    **#oc create secret generic mysecret --from-file htpasswd=user-details/users.config -n openshift-config**
               a. generic - is type of secret
               b. mysecret - secret name
3. for mysecret, yaml file will be created so to view the file **#oc get secret mysecret -o yaml -n openshift-config**

   <img width="1542" height="557" alt="image" src="https://github.com/user-attachments/assets/d162f9fd-93f3-4a59-a3c4-8135da2f18e5" />





   
 To get the pod details of another project(namespace) // -n -> namespace , openshift-authentication -> project name
whenever user gets created in openshift cluster, those details are maintained in oauth-pod under "openshift-authentication"
 namespace.
**#oc get pod -n openshift-authentication**
 <img width="1355" height="111" alt="image" src="https://github.com/user-attachments/assets/36542432-f2d4-4001-8ac4-3e607b2a332f" />
**oc get oauth cluster -o yaml**
