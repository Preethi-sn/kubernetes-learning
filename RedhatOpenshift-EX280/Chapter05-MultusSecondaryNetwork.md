# Multus Secondary Network



Creating sample Multus deployment

<img width="1351" height="337" alt="image" src="https://github.com/user-attachments/assets/e69997f5-a2e7-4eff-b2ac-01b8794e0205" />


Verifying the IP address of master node (here as per redhat example, we are taking ip address from ens4)

<img width="1150" height="247" alt="image" src="https://github.com/user-attachments/assets/971233a2-ef29-4cab-841d-1fd00101a661" />

Verifying the ethernet interface IP address of utility node(DB team jump host)

<img width="1320" height="132" alt="image" src="https://github.com/user-attachments/assets/27c6af4a-54d5-43d0-86ce-60f07459735b" />

We should be able to ping the IP address of both master and utility node from eachother.

Before creating the secondary network, we can verify that pod has only one eth0 interface created which is the primary interface.

<img width="1525" height="301" alt="image" src="https://github.com/user-attachments/assets/b1a55120-b5ee-4af4-9640-bf21af0eafdd" />

Create network attachment yaml file with required details

<img width="1540" height="587" alt="image" src="https://github.com/user-attachments/assets/19bb5172-d7fd-4f84-8ddb-dd2643976c72" />


Create the network attachment resource from the yaml file

<img width="1512" height="85" alt="image" src="https://github.com/user-attachments/assets/64b8b420-14c9-4985-86f4-a4caac43c1a2" />

Once secondary network created, we have to add the custom network resource in deployment yaml file as annotation ad redoply it

<img width="957" height="192" alt="image" src="https://github.com/user-attachments/assets/b475c6a9-370a-43c9-97f4-8648d6f28075" />


<img width="1242" height="237" alt="image" src="https://github.com/user-attachments/assets/b4651923-d9ae-4cbe-afb6-e228e811e123" />

Wait for resources get ready and check the secondary network got created as below

<img width="1521" height="482" alt="image" src="https://github.com/user-attachments/assets/e648626d-9763-4223-81bf-2272fea83b73" />


Now with that newly created secondary IP, we can be able to reach the DB app from utility host via psql command.

<img width="1207" height="542" alt="image" src="https://github.com/user-attachments/assets/5b62f7f7-4e8c-448c-aabc-fc11ac49341a" />

