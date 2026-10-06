# Application Security

scc constraints are applied to the container. It will determine the level of permission the application can access the underlying physical host/vm.

Like we have i) restricted constraint ii) anyuid constraint

Restricted mode will not allow the app to reach the root FS on the host, and it will allow the application to access the secure port(<1000) due to security reason.

anyuid mode, no blockage.


Deploying the GitLab application. But the pod went into error state while checking #oc log <pod-name>, found that the application is trying to reach the /etc folder 
but it failed due to permission denied.

<img width="1566" height="672" alt="image" src="https://github.com/user-attachments/assets/2182df48-5e6e-400b-8bbd-6162d880f67c" />


<img width="1587" height="217" alt="image" src="https://github.com/user-attachments/assets/6fe7418f-a3d1-4574-84c3-00e14168f89d" />

from this output, we can clearly see the pod is trying to restart multiple time to make it run but unfortunately, it went to crashloopbackoff error due to scc constraint

<img width="1522" height="240" alt="image" src="https://github.com/user-attachments/assets/d8aca705-3f9b-4e80-9014-a47104144fe4" />

we can check which scc constraint assigned to the pod #oc describe pod mysql-65f49c99-7pchc | grep scc

we can verify the suitable scc for the deployment and make the changes.

            oc get deploy <deployment-name> -o yaml | oc adm policy scc-subject-review -f -


To modify the scc constraint to any of the component in k8s, we have to do it via service account.

          oc create serviceaccount <sa-name>
          oc adm policy add-scc-to-user anyuid -z <sa-name> 
          oc set serviceaccount deployment/<deplo-name> <sa-name>
          
First, we should create service account and assign the role to SA and then set that service account to deployment.

As soon as we set the sa to deployment, pod comes to running state.


<img width="1525" height="417" alt="image" src="https://github.com/user-attachments/assets/a9a0b860-c678-414b-bf21-ac742b63c31d" />



<img width="1552" height="596" alt="image" src="https://github.com/user-attachments/assets/3882f856-04c1-4628-9380-024ae73b1e81" />
