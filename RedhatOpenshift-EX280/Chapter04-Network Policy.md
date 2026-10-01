# Network Policy

We can restrict the pod access by setting Network policies. Example, no other pods should access my pod, only specific pod can access my application and restrict all other pod. 

Based on our requirement we can create network policy using yaml file and apply.

## Deny-All Policy (Ingress policy)

Once application is deployed. Create yaml file for network policy. As per below file, under spec, podSelector: {} is empty. it means none of the pod should access this application (no ingress traffic) exist on the project demo10. and there wont we any restriction for egress policy.

Project nam is specified in metadata namespace.

                    cat deny-all.yaml
                    apiVersion: networking.k8s.io/v1
                    kind: NetworkPolicy
                    metadata:
                      name: deny-all 
                      namespace: demo10
                    spec: 
                      podSelector: {}

                    #oc create -f deny-all.yaml

<img width="1252" height="282" alt="image" src="https://github.com/user-attachments/assets/b5ce9f1d-b1e7-43d5-8642-8fdc28109f24" />


<img width="1391" height="467" alt="image" src="https://github.com/user-attachments/assets/dd801015-55b1-4b3c-83d6-f3703586f8c4" />
