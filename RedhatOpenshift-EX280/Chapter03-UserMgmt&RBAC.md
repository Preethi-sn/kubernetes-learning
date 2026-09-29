# Chapter:03 - User Management

<img width="1348" height="723" alt="user create flow mechanism" src="https://github.com/user-attachments/assets/4010df34-2e94-4824-a5f4-4ef9738268bd" />

1. Initiate lab: To make the cluster ready for the excerise
2. login with admini,developer,kubadmin
oc login -u kubeadmin -p yyUai-QPoXs-xBYSN-UJITn https://api.ocp4.example.com:6443
3. #oc new-project user-demo -> create new project
4. #oc whoami -t
## Step:1 - Create user using htpasswd tool
1. To create user, we have to use htpasswd tool. check if its installed (#htpasswd). If not, install it.
                     **sudo yum install httpd-tools -y**
2. Create directory **#mkdir user-details** directory name can be anything.
3. Create user, **#htpasswd -c -b -B user-details/users.config <username> <password>**
           -c - create users.config file (use this -c option when we are creating the user.config file first time. from next time dont use c as it will create new config file and delete the existing file and create new and old username will also get removed)
           -b - is to inject the user password in the file along with username
           -B - to secure the password safely in users.config file.
<img width="1521" height="410" alt="image" src="https://github.com/user-attachments/assets/fd9e4430-7975-447f-ba0c-3b77e37412e6" />

## Step:2 - Convert the user config into secrets and inject the secret in openshift-config namespace
1. To get the list of existing secrets in openshift-config namespace.
          #oc get secrets -n openshift-config
2. To create secret for user config file
          #oc create secret generic mysecret --from-file htpasswd=user-details/users.config -n openshift-config**
                 a. generic - is type of secret
                 b. mysecret - secret name
3. for mysecret, yaml file will be created so to view the file 
           #oc get secret mysecret -o yaml -n openshift-config

<img width="1565" height="652" alt="image" src="https://github.com/user-attachments/assets/5cc78b0c-8225-4834-804d-68419444cab1" />

## Step:3 - Syncup openshift-config and opendhift-authenticatgion through oauth file
If existing file is there we have to replace it else we have to create new oauth file.
1. View the oauth yaml file
       #oc get oauth cluster -o yaml
2.If the oauth.yaml file is not available in cluster by default, we have to create it else we can try to update the existing file with our secret if not we can replace the existing oauth with new oauth file.
3. vi oauth.yaml
```       
apiVersion: config.openshift.io/v1
kind: OAuth
metadata:
  name: cluster
spec:
  identityProviders:
  - name: my_first_IDP 
    mappingMethod: claim 
    type: HTPasswd
    htpasswd:
      fileData:
        name: mysecret 
```

In above yaml file, we are just mentioning secret name under fileData and provide the name for identityProvider. no other changes are required.
4. To get the oauth yaml file syntax. 
https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/authentication_and_authorization/configuring-identity-providers#identity-provider-htpasswd-CR_configuring-htpasswd-identity-provider
5. Once oauth file is ready. run the below command to replace it
              ```#oc replace -f oauth.yaml
                 #oc create -f oauth.yaml -> if want to create new file```
6. As soon as oauth file is replaced/updated, you can see the oauth pod restarted to syncup the update. 
              #oc get pod -n openshift-authentication
7. whatever users are added in user config, they can able to login now.
<img width="1530" height="472" alt="image" src="https://github.com/user-attachments/assets/9a02f3e8-1e5e-4282-8fb2-0bbdd3bddf2b" />

## Extract the secrets from cluster and add the new user in existing file
1. Unfortunately, if the user-details directory is deleted locally, we can extract it from cluster from openshift-config project.
              #oc extract secret/mysecret --to=Downloads/ -n openshift-config
2. It will be retrieved under Downloads directory with file name htpasswd. We can add the new user in existing file
              #htpasswd -b -B Downloads/htpasswd <username> <password>
<img width="1532" height="622" alt="image" src="https://github.com/user-attachments/assets/b115a830-14a6-429e-99fb-770ac5d9a45a" />
3. Whenever new user is added, it needs to be updated in secret (means from local to cluster).
              #oc set data secret/mysecret --from-file htpasswd=Downloads/htpasswd -n openshift-config
4. Onces its updated, we can see the oauth pod will get synced up as a reflecting of cluster updation
<img width="1542" height="486" alt="image" src="https://github.com/user-attachments/assets/00292e38-a2df-4018-b663-b659361cbbae" />

 5.Command to delete the secrets:
               #oc delete secret mysecret -n openshift-config
 

 To get the pod details of another project(namespace) // -n -> namespace , openshift-authentication -> project name
whenever user gets created in openshift cluster, those details are maintained in oauth-pod under "openshift-authentication"
 namespace.
**#oc get pod -n openshift-authentication**
 <img width="1355" height="111" alt="image" src="https://github.com/user-attachments/assets/36542432-f2d4-4001-8ac4-3e607b2a332f" />


To get the Users list and IDP details
<img width="1542" height="592" alt="image" src="https://github.com/user-attachments/assets/bcfbaaeb-ea2b-45d7-aace-5cecde81defb" />








