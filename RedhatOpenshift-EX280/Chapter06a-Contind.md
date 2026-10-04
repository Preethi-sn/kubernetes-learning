# Set the quota for particular project and set the limit range for pod

If we set the quota limit to project and try to deploy app it wont work. We have to create Limit Range for the pod resource in declarative way.

<img width="1411" height="377" alt="image" src="https://github.com/user-attachments/assets/5196d846-808b-485f-9eef-e8aeafaab371" />

<img width="1522" height="446" alt="image" src="https://github.com/user-attachments/assets/8691c17d-f6cb-4925-8ca3-22b42c150882" />

Below error is from #oc get events

<img width="1542" height="340" alt="image" src="https://github.com/user-attachments/assets/5585ef7b-e773-4502-b063-8601d5dbc2f9" />

Creating the Limit Range resource

```
cat > limits.yaml
apiVersion: "v1"
kind: "LimitRange"
metadata:
  name: "resource-limits" 
spec:
  limits:
    - type: "Container" 
      max:
        cpu: "500m"
      min:
        cpu: "100m"
      default: 
        cpu: "200m"
```

Onces the file is ready, we have to create the resource. #oc create -f limits.yaml 

<img width="942" height="112" alt="image" src="https://github.com/user-attachments/assets/fe54bc85-21e8-4414-83aa-bfd9050e9f51" />

Once the limit range is created for the pod, we can able to deploy the application and not deployment and pod can run without any issue.

        oc new-app --name=apache-1 --image=quay.io/redhattraining/hello-world-nginx

<img width="1537" height="337" alt="image" src="https://github.com/user-attachments/assets/3c785ae1-76c0-4934-9b28-225c7006f8ee" />

Here we can clearly see the quota allocated for the project vs limit range set for container

<img width="1401" height="442" alt="image" src="https://github.com/user-attachments/assets/b969dbce-d9ba-4bde-ab02-ac94de5e7b6f" />

We can also try to deploy another application on the project and check the project quota

<img width="1430" height="207" alt="image" src="https://github.com/user-attachments/assets/b79c554d-c96b-4f34-b1f0-d199414276d6" />




