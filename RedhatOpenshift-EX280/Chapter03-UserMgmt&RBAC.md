**Chapter:03 - User Management**
1. Initiate lab: To make the cluster ready for the excerise
2. login with admini,developer,kubadmin
oc login -u kubeadmin -p yyUai-QPoXs-xBYSN-UJITn https://api.ocp4.example.com:6443
3. #oc new-project user-demo -> create new project
4. #oc whoami -t
5. To create user, we have to use htpasswd tool. check if its installed (#htpasswd). If not, install it.
       **sudo yum install httpd-tools -y**
6. Create directory **#mkdir user-details** directory name can be anything.
7. Create user, **#htpasswd -c -b -B user-details/users.config <username> <password>**
           //**-c** - create users.config file (use this -c option when we are creating the user.config file first time. from next time dont use c as it will create new config file and delete the existing file and create new and old username will also get removed)
          //**-b** - is to inject the user password in the file along with username
          //**-B** - to secure the password safely in users.config file.


   
 To get the pod details of another project(namespace) // -n -> namespace , openshift-authentication -> project name
whenever user gets created in openshift cluster, those details are maintained in oauth-pod under "openshift-authentication"
 namespace.
**#oc get pod -n openshift-authentication**
 <img width="1355" height="111" alt="image" src="https://github.com/user-attachments/assets/36542432-f2d4-4001-8ac4-3e607b2a332f" />
**oc get oauth cluster -o yaml**
