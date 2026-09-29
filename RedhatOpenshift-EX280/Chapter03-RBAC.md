# RBAC- Role Based Access Control
Default roles in clusters are, admin, view, edit which is similar to rwx in linux file permissions

By default, every new user getting created in Opensshift cluster, will get a prompt to create new project. That is because, every user is added to the group 
"system:authenticated:oauth" and this group is having role "self-provisioner"

              Group : "system:authenticated:oauth" 
              Cluster Role: "self-provisioner"

To list the group which are having cluster role binding role assigned
           ``` oc get clusterrolebinding -o wide | grep -E 'ROLE|self-provisioner'  ```

Confirm self-provisioner cluster role assigned to the system:authenticated:oauth group
       ```   #oc describe clusterrolebindings self-provisioners ```

Remove the cluster rule from group as below:
         ``` #oc adm policy remove-cluster-role-from-group self-provisioner system:authenticated:oauth ```
Once its removed userever user logged in will not get the promt to create new project(not allowed to create project)

