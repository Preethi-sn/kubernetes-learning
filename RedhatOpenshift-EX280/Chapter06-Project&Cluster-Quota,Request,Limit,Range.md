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


create insecure rotue and try to do the load test

<img width="1527" height="261" alt="image" src="https://github.com/user-attachments/assets/e1da8e33-614e-4b97-8a20-dcd519edafd9" />


```
 Load test by trying to access the app multiple time with 200mi memory:
  #curl -X GET http://testapp-demo13.apps.ocp4.example.com/api/loadtest/v1/mem/200/60
 We can monitor the status of pod that it goes under restart multiple time #watch oc get pod and comes back to running state after the load gets dowm.
```

<img width="1522" height="217" alt="image" src="https://github.com/user-attachments/assets/abf5542f-7ab0-45c9-857b-34eadcccec6f" />


<img width="1540" height="185" alt="image" src="https://github.com/user-attachments/assets/3d879d17-88b4-428d-b188-e786266bacc6" />

