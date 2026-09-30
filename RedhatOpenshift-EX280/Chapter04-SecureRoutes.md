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









