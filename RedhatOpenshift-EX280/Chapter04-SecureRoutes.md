# Secure Routes

There are 3 types of secure routes.
        ```
           i) Edge termination
           ii) Reencrypt termination
           iii) Passthrough termination
        ```

**Edge Termination:** TLS traffic will be secure till loadbalancer(Haproxy) and from loadbalancer to pod it will be plain traffic

**Reencrypt Termination:** TLS traffic will be secure from client to LBas well as secure from LB to pod.

**Passthrough Termination:** It bypass LB(haproxy) and directly reaches pd and L will not interrupt the request. secure traffic will be handled at pod level by attaching the certificate. So, clients can communication with pod through certificates.

Mostly organization expose their applicaion using passthrough termnation method.

## Passthorugh Method:

### 1. Create CSR file(certificate Signing Request) and key

<img width="1542" height="477" alt="image" src="https://github.com/user-attachments/assets/b5c3fbc6-844b-4cd0-ba97-2d52f40e3441" />

### 2. Create CRT file using CSR and key file

<img width="1525" height="712" alt="image" src="https://github.com/user-attachments/assets/4835f86b-ba12-4408-a52e-d17e4e90b22b" />


### 3. Create secret with type TLS to store these files. 

<img width="1537" height="362" alt="image" src="https://github.com/user-attachments/assets/7fa2f494-2c44-4b3c-9bca-2497c87ce381" />


### 4. Application is deployed

<img width="1542" height="656" alt="image" src="https://github.com/user-attachments/assets/b4863ecc-3891-43d0-b4eb-a32fd294e505" />


### 5. Deployed application went into crashloopbackoff error and log says SSL certificate doesn't exist.

This because we didn't inject the certificates in the deployment.

<img width="1531" height="790" alt="image" src="https://github.com/user-attachments/assets/09ad093f-2f51-4acf-ac05-ac97f4da0ffb" />

we converted certificates as secrets so that should be mounted as volume in the specified location.

<img width="1537" height="190" alt="image" src="https://github.com/user-attachments/assets/61f0b35f-e4dd-4e2d-a39b-952217504513" />

As soon as we mount the secret as volume, pod is up and running.

<img width="1347" height="232" alt="image" src="https://github.com/user-attachments/assets/1b73741a-5545-4c3d-82e5-60e630eb5920" />


Now we have to create passthrough secure route. With this route hostname "phpsecure.apps.ocp4.example.com" we can access the applicaion in browser as https://phpsecure.apps.ocp4.example.com

<img width="1527" height="407" alt="image" src="https://github.com/user-attachments/assets/88ba2cb1-b212-42f3-9056-e00410f279a4" />









