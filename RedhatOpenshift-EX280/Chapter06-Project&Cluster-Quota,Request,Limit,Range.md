# Project and Cluster Quota

## Set the request and limit for particular pod:

This is the standard resource request for memory 10mi minimum.

<img width="1302" height="112" alt="image" src="https://github.com/user-attachments/assets/b868275d-9183-4ef2-a3f0-110835cc2013" />


Setting the higher value to pod which leads to pod not able to run

<img width="1531" height="162" alt="image" src="https://github.com/user-attachments/assets/0202f5e6-7e81-4acd-ab64-04ec23ecdddd" />


<img width="1516" height="181" alt="image" src="https://github.com/user-attachments/assets/526da048-977a-4e1f-9e83-cedf1950509c" />

By setting limit, we are telling the maximum memory quota the pod can consume from underlying machine/node. 

<img width="1477" height="107" alt="image" src="https://github.com/user-attachments/assets/e6026393-4678-4fea-9a0d-d6701f95be66" />

If you see the #oc describe pod <podname>, we can see the request and limit set for the pod.

<img width="712" height="162" alt="image" src="https://github.com/user-attachments/assets/794101a4-5210-4e8e-a267-080991230824" />

```
   #oc new-app --name testapp --image=quay.io/redhattraining/loadtest
  #oc set resources --requests memory=10Mi deployment/testapp --> set the standard request 
  #oc describe node master01
  #oc set resources --requests memory=10Gi deployment/testapp --> set the higher value request pod unable to run
  #oc describe pod testapp-5cc69f758c-bxknr
  #oc set resources --requests memory=10Mi deployment/testapp  --> change to existing stage
  #oc set resources  --limits memory=100Mi deployment/testapp  --> set the limits
````

create insecure rotue and try to do the load test

<img width="1527" height="261" alt="image" src="https://github.com/user-attachments/assets/e1da8e33-614e-4b97-8a20-dcd519edafd9" />


```
 Load test by trying to access the app multiple time with 200mi memory:
  #curl -X GET http://testapp-demo13.apps.ocp4.example.com/api/loadtest/v1/mem/200/60
 We can monitor the status of pod that it goes under restart multiple time #watch oc get pod and comes back to running state after the load gets dowm.
```

<img width="1522" height="217" alt="image" src="https://github.com/user-attachments/assets/abf5542f-7ab0-45c9-857b-34eadcccec6f" />


<img width="1540" height="185" alt="image" src="https://github.com/user-attachments/assets/3d879d17-88b4-428d-b188-e786266bacc6" />

## Set the quota for particular project:

Setting quota limit to particular project and check the currently used and available quota

               #oc create quota project-quota --hard pods=5,services=5,secrets=15,configmaps=5
               #oc describe quota project-quota 


<img width="1512" height="85" alt="image" src="https://github.com/user-attachments/assets/60e24e89-cb2c-4355-8178-6436f3481e07" />


<img width="1017" height="320" alt="image" src="https://github.com/user-attachments/assets/6e3ed25c-662e-4997-8344-5082010c4cc2" />


As soon as we deployed application and scale up the pod, quota value gets changed and we can't increase beyond the quota limit

<img width="1300" height="360" alt="image" src="https://github.com/user-attachments/assets/8c7f1095-6a1a-4e35-853c-c4f5c1a57b6a" />





