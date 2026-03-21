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

We will add rules to all of the networks to simulate real network segmentation. select Firewall -> Rules -> Client, click add(+). 

<img width="1230" height="927" alt="image" src="https://github.com/user-attachments/assets/7f590ba1-793d-4815-88f4-20c0653ab29b" />

For the Client net the rules go as follows: Set Action: Pass, Interface: Client, Protocol: Any, Source: Client net, and Destination: any. Set Action: Pass, Interface: Client, Protocol: Any, Source: Client net, and Destination: Server net. For the DMZ net the rules go as folows: Action: Block, Interface: DMZ, Protocol: IPv4, Source: DMZ net, and Destination: Client net. Action: Block, Interface: DMZ, Protocol: IPv4, Source: DMZ net, and Destination: Server net. Action: Pass, Interface: DMZ, Protocol: IPv4, Source: DMZ net, and Destination: Any. Finally, the Server rules go as follows: Action: Pass, Interface: Server, Protocol: IPv4, Source: Server net, and Destination: Any. 

Now I will add the Winodws 10 virtual machine and the Windows Active Directory Server. Create a new virtual machine with the Windows 10 iso image. I gave my machine 4096 MB and 1 CPU ad secleted skip unintended install. 

<img width="940" height="725" alt="image" src="https://github.com/user-attachments/assets/7138ce8e-26a2-476d-ad97-e912b06985a3" />

Power up the virtual machine and start the configuration process until prompted to activate Windows. Select I dont have a product key -> Windows 10 Pro. Click custom install to install Windows 10 only. Allow that installation to finish.

Now I will install the active directory server to do this download the Winodows 2022 server from the Windows website. Create a new machine and instert the iso image that was downloaded from the Windows website. Click skip unintended installation, next select finish to boot up the virtual machine.

<img width="945" height="717" alt="image" src="https://github.com/user-attachments/assets/7cc49d30-288b-4f70-ba32-4c3cbe1e7fa0" />

When the machine has started go through the configuration that is wanted then when prompted to ask for a version. Select the standard Evaluation Windows Server and select custom install. Wait for the installation to finish.

<img width="1022" height="847" alt="image" src="https://github.com/user-attachments/assets/716fe61d-0cae-4b7c-93de-86c877cbc339" />

When finished it will prompt the user to enter in a password then select finish. 

<img width="1022" height="856" alt="image" src="https://github.com/user-attachments/assets/26dbd1e4-4c6b-44ef-9859-d0fc61c457bc" />

