# RBAC- Role Based Access Control
Default roles in clusters are, admin, view, edit which is similar to rwx in linux file permissions

By default, every new user getting created in Opensshift cluster, will get a prompt to create new project. That is because, every user is added to the group 
"system:authenticated:oauth" and this group is having role "self-provisioner"

              Group : "system:authenticated:oauth" 
              Cluster Role: "self-provisioner"

To list the group which are having cluster role binding role assigned

           `oc get clusterrolebinding -o wide | grep -E 'ROLE|self-provisioner'  

Confirm self-provisioner cluster role assigned to the system:authenticated:oauth group

         #oc describe clusterrolebindings self-provisioners 

Remove the cluster rule from group as below:

         #oc adm policy remove-cluster-role-from-group self-provisioner system:authenticated:oauth
         
Once its removed userever user logged in will not get the promt to create new project(not allowed to create project)

Login to project/create new project and Grand project administrator privilege to user

          oc get project <project_name> or oc new-project <project-name>
          oc policy add-role-to-user admin leader

Creating new group and add respective engineers in their group

<img width="1295" height="556" alt="image" src="https://github.com/user-attachments/assets/d8e12c82-06d5-4405-b0af-6b25090f396c" />

Provide the write(edit) and read(view) access to the group based on the request

<img width="1407" height="360" alt="image" src="https://github.com/user-attachments/assets/b337e3bd-2563-434b-ad1b-16480acccb3d" />


Whoever is having the write access they can be able to deploy the app on that project and make updates/changes to the resources created but they can provide privilege to other users rather than admin user.

We can also restore the Self-provisioner role to the group which revoke earlier

oc adm policy add-cluster-role-to-group --rolebinding-name self-provisioners self-provisioner system:authenticated:oauth








          
