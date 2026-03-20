# SIEM-Lab---Opnsense-Firewall-Network-Segmentation
In this project I will be updating my opnsense network to have network segmentation. This is the diagram of how the new network will look after the implementation of network segmentation. 

<img width="782" height="520" alt="image" src="https://github.com/user-attachments/assets/bfcde3ab-07f2-48b6-b1c4-46e931a9ef91" />

The first thing that must be done is add new internal networks adapters to the firewall. This is done by navigating to the settings and enabling all four network adapters and naming them intnet-client, intnet-server, and intnet-DMZ. Each network will host different machines. As seen in the diagram the client side will hold a windows 10 virtual machine. The server side will hold the Wazuh server and the active directory server. Then the demilitarized zone will hold the kali linux virtual machine. 

Then we will navigate to the kali linux machine and assign the different interfaces. This is done by logging into the opnsense firewall login page and navigating to interfaces and assignments. Then select each of the network adapters(em1, em2, em3) and name them client, server, and DMZ respectively. 

<img width="998" height="355" alt="image" src="https://github.com/user-attachments/assets/cc23f8f2-bd66-4a3a-a611-d5e9a0599a5d" />

Select save and interfaces and the names of each of the subnetworks should be displayed as follows.

<img width="198" height="377" alt="image" src="https://github.com/user-attachments/assets/2bfe8738-6ec0-4e0f-9c0d-9573b223efee" />

Select each individual subnetwork and select enable interface, set all of the ipv4 address to 10.200.10.1/24, 10.200.20.1/24, and 10.200.30.1/24 respectively. Save these settings navigate to the firewall, assign the interfaces as was done in the previous steps. When all networks have been accounted for, the result should look like this.

<img width="718" height="317" alt="image" src="https://github.com/user-attachments/assets/58e6fb6d-6a25-4e86-b9cb-daa6fb5d4e9f" />

