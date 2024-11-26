# VLAN and Inter-VLAN Routing Configuration

## Objective

In this lab I will perform a VLAN configuration for campus network, including Virtual Trunking Protocol, Access and Trunk ports, and inter-VLAN routing the main objective of this lab exercise is to configure and manage VLANs (Virtual Local Area Networks) within a campus network to enhance network segmentation, scalability, and security.


### Skills Learned

- Understanding VLANs and Their Benefits
- Segmenting the network logically regardless of physical layout.
- Configuring VLANs on Switches
- Implementing Virtual Trunking Protocol (VTP)
- Setting Up Access and Trunk Ports
- Implementing Inter-VLAN Routing
- Troubleshooting VLAN Configurations
- Deeper understanding of VLAN configuration best practices


### Tools Used

- Cisco IOS Vendor-specific CLI 
- Layer 2 or Layer 3 Switches (Physical or Virtual)
- Routers (Physical or Virtual)
- GNS3: For simulating network devices and configurations.
- Cisco Packet Tracer: Simplified tool for learning and configuring VLANs.
- PuTTY (Terminal Emulator Software)

## Steps

# Lab Topoplogy
![image](https://github.com/user-attachments/assets/9895d11a-b481-4795-9a52-c8f56c86c280)

## VTP, Access and Trunk Ports

1) All routers and switches are in a factory default state. View the VLAN database on SW1 to verify no VLANs have been added.
![image](https://github.com/user-attachments/assets/1c42da38-5cad-45a7-b029-641b6dd136c8)

2) View the default switchport status on the link from SW1 to SW2.
![image](https://github.com/user-attachments/assets/b31244bd-327b-4193-8322-bd0a83f71dba)



The trunking mode is set to dynamic auto and the interface is currently in the access port operational mode using default VLAN 1.

3) Configure the links between switches as trunks.
![image](https://github.com/user-attachments/assets/72efd4c7-609d-411f-9297-682b4170bd8e)
![image](https://github.com/user-attachments/assets/f1edf1a2-6d82-449d-b158-b83172c80f8e)
![image](https://github.com/user-attachments/assets/79cb7e47-f799-4093-8875-a0ac2085a3a1)
![image](https://github.com/user-attachments/assets/816b59d5-26d4-4918-b0c6-127164e7a2c5)

4) Configure SW1 as a VTP Server in the VTP domain Flackbox.
![image](https://github.com/user-attachments/assets/362d4860-9d59-4a89-b780-d31b4454259e)

5) SW2 must not synchronise its VLAN database with SW1.
![image](https://github.com/user-attachments/assets/f774743a-521c-4545-a768-a130bf16c586)

6) SW3 must learn VLAN information from SW1. VLANs should not be edited on SW3.
![image](https://github.com/user-attachments/assets/c4e2732c-9cbf-497e-9bdc-8f27057d6bbf)

7) Add the Eng, Sales and Native VLANs on all switches.

VLANs must be configured on the VTP Server SW1 and on VTP Transparent SW2. VTP Client SW3 will learn the VLANs from SW1.
![image](https://github.com/user-attachments/assets/abfbbb42-cfed-44bf-95ba-9065f33e7481)

8) Verify the VLANs are in the database on each switch.
![image](https://github.com/user-attachments/assets/8f67f498-85b6-4ac7-b2b9-1b69ebc730db)

9) Configure the trunk links to use VLAN 199 as the native VLAN for better security.
![image](https://github.com/user-attachments/assets/fc924c59-54af-47e5-8c20-873790867cb0)
![image](https://github.com/user-attachments/assets/4f87fb9a-ed8b-44af-b7c0-0bbe9c27024d)
![image](https://github.com/user-attachments/assets/44cf0211-00ae-4e3b-a9f1-fd79590cc845)

10) Configure the switchports connected to the PCs with the correct VLAN configuration.

Eng PCs should be in VLAN 10, Sales PCs in VLAN 20
![image](https://github.com/user-attachments/assets/96b45e19-8276-4ec5-873f-bd4718b56aff)

11) Verify the Eng1 PC has connectivity to Eng3.
![image](https://github.com/user-attachments/assets/1c4aa257-1688-4387-ab41-3b88c7e2ee9f)

12) Verify Sales1 has connectivity to Sales3.
![image](https://github.com/user-attachments/assets/067c6fc3-29ec-40a2-9a95-ef012d779f7d)

## Inter-VLAN Routing – Option 1 Separate Interfaces on Router

13) Configure interface FastEthernet0/0 on R1 as the default gateway for the
Eng PCs.
14) Configure interface FastEthernet0/1 on R1 as the default gateway for the
Sales PCs.
15) Configure SW2 to support inter-VLAN routing using R1 as the default
gateway.
16) Verify the Eng1 PC has connectivity to the VLAN 20 interface on R1.
17) Verify the Eng1 PC has connectivity to Sales1.
18) Clean-up: Shut down interface FastEthernet0/1 on R1.

## Inter-VLAN Routing – Option 2 Router on a Stick


19) Configure sub-interfaces on FastEthernet0/0 on R1 as the default
gateway for the Eng and Sales PCs.
20) Configure SW2 to support inter-VLAN routing using R1 as the default
gateway.
21) Verify the Eng1 PC has connectivity to the VLAN 20 interface on R1.
22) Verify the Eng1 PC has connectivity to Sales1.
23) Clean-up: Shut down interface FastEthernet0/0 on R1.


## Inter-VLAN Routing – Option 3 Layer 3 Switch

24) Enable layer 3 routing on SW2.
25) Configure SVIs on SW2 to support inter-VLAN routing between the Eng
and Sales VLANs.
26) Verify the Eng1 PC has connectivity to the VLAN 20 interface on SW2.
27) Verify the Eng1 PC has connectivity to Sales1.



