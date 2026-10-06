
Auto Scaling: Whenever the load gets increased, application needs to be scaled up and down during non-peak hours.

Here we are setting request and limit to cpu. if it crossed more than 60% , pods need to be scaled up

<img width="1547" height="521" alt="image" src="https://github.com/user-attachments/assets/0b37e721-c459-4011-ac90-a74d34afd6bf" />

                                  oc describe deployment testapp | grep -A1 -E 'Requests|Limits'
                                  oc set resources --requests cpu=10m --limits cpu=100m deployment/testapp
                                  oc describe deployment testapp | grep -A3 -E 'Requests|Limits'
                                  oc autoscale --min=3 --max=15 --cpu-percent=60 deployment/testapp
                                  oc get hpa

<img width="1442" height="256" alt="image" src="https://github.com/user-attachments/assets/4bdc27e4-3fc4-43cb-a88f-365b5b3cd528" />


                      curl -X GET http://<route-name>/api/loadtest/v1/cpu/1
                      

 <img width="1115" height="302" alt="image" src="https://github.com/user-attachments/assets/7b2fe5fd-b30f-499b-959d-0761df0bd675" />


  <img width="1552" height="265" alt="image" src="https://github.com/user-attachments/assets/d3f28414-c2bd-4106-8d88-aea144415893" />
