# RBAC- Role Based Access Control
Default roles in clusters are, admin, view, edit which is similar to rwx in linux file permissions

By default, every new user getting created in Opensshift cluster, will get a prompt to create new project. That is because, every user is added to the group 
"system:authenticated:oauth" and this group is having role "self-provisioner"
