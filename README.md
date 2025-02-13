# Cisco – VLAN and Inter-VLAN routing configuration LAB

## Objective

In this lab I performed real-world networking experience with VLAN deployment and inter-VLAN routing for a campus network, which is crucial for enterprise networking, network automation, and even cloud-based networking solutions, including Virtual Trunking Protocol (VTP), Access and Trunk ports, and inter-VLAN routing (Option 1 – Separate Interfaces on Router, Option 2 – Router on a Stick and Option 3 – Layer 3 Switch)


### Skills Learned

-	Creating VLANs and assigning ports to specific VLANs.
-	Understanding VLAN segmentation to separate network traffic.
-	Configuring VLAN naming conventions for better network management.
-	Configuring VTP domains and ensuring proper VLAN propagation.
-	Configuring switchports correctly based on their role in VLAN communication.
-	Configuring Inter-VLAN routing
-	Diagnosing VLAN connectivity issues
-	Ensuring proper security configurations on VLANs.


### Tools Used

-	Cisco IOS Command Line Interface (CLI)
-	GNS3 for simulated network devices (e.g., routers, PCs, or switches) to test


*Ref 1: Network Diagram*
![image](https://github.com/user-attachments/assets/81d10ebf-c239-4736-bdb0-15609f78ae9a)

 
### STEPS



### VTP, Access and Trunk Ports


1)	All routers and switches are in a factory default state. View the VLAN database on SW1 to verify no VLANs have been added.

![image](https://github.com/user-attachments/assets/0ad53680-3b41-400e-904a-b07c66c4c9bd)


2)	View the default switchport status on the link from SW1 to SW2

![image](https://github.com/user-attachments/assets/a2ee8ab9-92d8-4a86-9ade-7fab51ae9931)

 
The trunking mode is set to dynamic auto and the interface is currently in the access port operational mode using the default VLAN 1.

3)	Configure the links between switches as trunks.

![image](https://github.com/user-attachments/assets/73313204-e6c8-4250-b255-02b4d00937fd)

SW2

![image](https://github.com/user-attachments/assets/647b8b8f-65c3-4b20-9741-ca624c0cc23a)

SW3

![image](https://github.com/user-attachments/assets/653d2033-0596-47ae-b09e-3db8ae7532c5)



4)	Configure SW1 a VTP Server in the VTP domain Sky29
![image](https://github.com/user-attachments/assets/198d3c8f-435c-4e5c-befe-6a25a6f9539f)
 
 

5)	SW2 must not synchronise its VLAN database with SW1

![image](https://github.com/user-attachments/assets/6bdc2d65-842f-403a-a456-7f621283f708)

6)	SW3 must learn VLAN information from SW1. VLANs should not be edited on SW3.

![image](https://github.com/user-attachments/assets/a3b440e2-e840-403a-9b6c-bd413bc9365c)


7)	Add the Engineering, Sales and Native VLANs on all switches.
VLANs must be configured on the VTP Server SW1 and on VTP Transparent SW2. VTP Client SW3 will learn the VLANs from SW1.

![image](https://github.com/user-attachments/assets/ce8cdf24-927a-4a42-8b1a-d97c7ea944c4)
![image](https://github.com/user-attachments/assets/5c2c52b7-bf61-4c2e-b90b-faf7717cf159)




8)	Verify the VLANs are in the database on each switch.

![image](https://github.com/user-attachments/assets/d6e54c22-03a4-44f3-bbad-0a05713eadb0)


9)	Configure the trunk links to use VLAN 199 as the native VLAN for better security.

![image](https://github.com/user-attachments/assets/5158e8a8-dab8-494c-872e-0052261232ce)
![image](https://github.com/user-attachments/assets/392f02d3-0e02-41b5-b54f-b5ec66f58b04)
![image](https://github.com/user-attachments/assets/a85f98b0-b1e8-42eb-9688-8e2c96e3dc3b)
![image](https://github.com/user-attachments/assets/fecbef64-d296-41b5-94a5-490919b60257)



10)Configure the switchports connected to the PCs with the correct VLAN configuration.


- Engineering PCs should be in VLAN 10, Sales PCs in VLAN 20

![image](https://github.com/user-attachments/assets/0be4bb8a-0863-4163-ac81-cd71f16a2d5c)

![image](https://github.com/user-attachments/assets/d4cc1f82-0a49-4e0f-b607-f710d038bd69)



11)	Verify the Engineering – PC1 has connectivity to Engineering – PC3

![image](https://github.com/user-attachments/assets/b27a6ce6-5de9-4033-8fef-25c19a9513f2)

 
12)	Verify the Sales – PC1 has connectivity to Sales – PC3

![image](https://github.com/user-attachments/assets/768df406-004f-4a4d-b741-ee5d47bba63e)


## Inter-VLAN Routing – Option #1 Separate Interfaces on Router


13)	Configure interfaces Fe0/0 on R1 as the default gateway for the Engineering PCs.

![image](https://github.com/user-attachments/assets/940e71e2-078f-4e8d-b168-aa7d36c58be0)

14)	Configure interfaces Fe1/0 on R1 as the default gateway for the Sales PCs.

![image](https://github.com/user-attachments/assets/d50daead-c46e-4180-9e4f-70fde5d2b901)


15)	Configure SW2 to support inter-VLAN routing using R1 as the default gateway.

![image](https://github.com/user-attachments/assets/accf550e-5d4e-4760-ba9a-bc9345e29a45)

 
16)	Verify the Engineering-PC1 has connectivity to the VLAN 20 interface on R1.

![image](https://github.com/user-attachments/assets/f7e9a583-a642-4894-bb42-5c5518d708e3)


17)	Verify the Engineering-PC1 has connectivity to Sales-PC1.

![image](https://github.com/user-attachments/assets/903760b5-d18b-4969-996f-12ebf79e2d28)


18)	Clean-up: Shut down interface Fe1/0 on R1

![image](https://github.com/user-attachments/assets/850c80c1-0adb-446e-a0e0-60dae59ed9bc)


 
## Inter-VLAN Routing – Option #2 Router on a Stick


19)	Configure sub-interfaces on Fe0/0 on R1 as the default gateway for Engineering and Sales PCs.

![image](https://github.com/user-attachments/assets/2311bb80-3813-4e34-9753-a82442f7aff8)
![image](https://github.com/user-attachments/assets/485dddee-671b-41d0-aff9-fe06e4095fdf)


20)	Configure SW2 to support inter-VLAN routing using R1 as the default gateway.

![image](https://github.com/user-attachments/assets/9b1c9349-bd85-4abf-9731-1b52227085de)


21)	Verify the Engineering-PC1 has connectivity to the VLAN 20 interface on R1.

![image](https://github.com/user-attachments/assets/4b74654a-477e-4516-9f86-2682e6f8ff02)


22)	Verify the Engineering-PC1 has connectivity to Sales-PC1.

![image](https://github.com/user-attachments/assets/f24d633b-60d1-48ea-9e9e-f07005993a27)


23)	Clean-up: Shut down interface Fe0/0 on R1

![image](https://github.com/user-attachments/assets/c6fba2e4-4de7-4ab6-a679-7ec6b80a78f3)




## Inter-VLAN Routing – Option #3 Layer 3 Switch


24)	Enable Layer 3 routing on SW2

![image](https://github.com/user-attachments/assets/6b96ef38-050b-47b6-b490-461ee6e08b1f)


25)	Configure SVIs on SW2 to support inter-VLAN routing between the Engineering and Sales VLANs.

![image](https://github.com/user-attachments/assets/3f7050fa-6761-410f-b088-16fdc6d7a5db)

 
26)	Verify the Engineering-PC1 has connectivity to the VLAN 20 interface on SW2.

![image](https://github.com/user-attachments/assets/3a7bbd21-1dc0-4d0d-97b5-c864ace07052)

27)	Verify the Engineering-PC1 has connectivity to Sales-PC1.

![image](https://github.com/user-attachments/assets/7205bf48-a07b-441d-a269-d69cab6e3b06)



