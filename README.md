# Mikrotik Simulation  
## VirtualBox 6.1.50 (on Linux)  
## Mikrotik RouterOS: 6.49.17  
## WinBox  

### Simulate MikroTik RouterOS in VirtualBox and configure it via Winbox  

### Create a virtual machine file
Click New  
![1](https://github.com/user-attachments/assets/c6c9406f-7b0a-4bca-8428-d5df4db73ee6)  
Enter the name, in this case, use 'Mikrotik' and then click Next  
![2](https://github.com/user-attachments/assets/3f8a897b-0e16-4374-a1c5-016921354886)  
Set the memory size to 512 MB (optional)  
![3](https://github.com/user-attachments/assets/fb0393f5-c1e1-43a4-8d8e-0c55941435ad)  
Choose 'Create a virtual hard disk now'  
![4](https://github.com/user-attachments/assets/5c116f95-8b96-42e2-a416-17c0ffa76016)  
Choose 'VDI (VirtualBox Disk Image)'  
![5](https://github.com/user-attachments/assets/04c9fb74-eb1a-4712-88a8-22c29f7f3739)  
Choose 'Dynamically allocated'  
![6](https://github.com/user-attachments/assets/1efe0d84-ec6f-41e1-a756-03ea72672cab)  
Set 2 GB (optional)  
![7](https://github.com/user-attachments/assets/862cc3b5-6123-469b-936d-85233bf7e88d)  
Enable both Adapter 1 and Adapter 2, then choose NAT  
NAT (Network Address Translation) is chosen in VirtualBox to provide internet access to the virtual machine (VM) through the host machine. It allows the VM to share the host's IP address, making it easy to set up without complex network configuration.  
![8](https://github.com/user-attachments/assets/7cbda8ed-56ae-4610-b1bb-6cd11c701576)  
Enable Adapter 3 and choose Host-only Adapter (optional)  
![9](https://github.com/user-attachments/assets/4595c055-7369-4a4d-ae22-bb839354a97d)  
Click OK, and then press Start  
### Start the virtual machine  
Click the icon pointed to by the arrow.  
![10](https://github.com/user-attachments/assets/e1cd91cf-48bb-4834-a91c-dc6fc8d7c979)  
Click Add  
![11](https://github.com/user-attachments/assets/c3cca75b-71d2-4773-992e-d7b177d1c8d4)  
Select the MikroTik RouterOS ISO file  
![12](https://github.com/user-attachments/assets/e98df8b7-2266-4b66-b57e-c7a02a8bd87b)  
Click Choose  
![13](https://github.com/user-attachments/assets/8598a927-16af-4fc1-9c37-9b51e30f305a)  
Click Start  
![14](https://github.com/user-attachments/assets/c59b3d5d-2e29-4457-8674-1e76a76e1ee0)  
Choose the software installation option  
In this case, press 'a' to select all, then press 'i' to install.  
![15](https://github.com/user-attachments/assets/dfd7d6a6-a345-414f-a05c-8114424694eb)  
Press 'n' for 'Do you want to keep the old configuration?' and then press 'y' to Continue  
Before rebooting, right-click the icon pointed to by the arrow, then click the MikroTik RouterOS ISO file  
![16](https://github.com/user-attachments/assets/6abec516-53a2-4bb5-bff8-c4e36b06b6a8)  
Force Unmount  
After installing MikroTik RouterOS, we need to force unmount the installation media (ISO) to prevent the virtual machine from booting from it again. This ensures the VM boots from the hard disk where RouterOS is installed, avoiding boot errors or conflicts.  
![17](https://github.com/user-attachments/assets/4fdc2650-f1ce-40bb-b0f9-3e0ebe7b0cb2)  
### Login to MikroTik, default user is 'admin' and the password is empty  
![17-2](https://github.com/user-attachments/assets/cfaec642-037a-44d1-9fd6-f53aa91264e1)  
Press 'n' for 'Do you want to see the software license' option  
![18](https://github.com/user-attachments/assets/5811a267-f1d7-4cbe-b0bc-99b0d1204d4f)  
We need to set a new password  
![19](https://github.com/user-attachments/assets/ebd1f1c5-6f25-4ec6-af9f-aacd23fb8cd3)  
### Open WinBox  
Select the IP address; it should be 0.0.0.0 because the IP has not been set yet. If an error occurs, look for another IP with the same MAC address or the same Board's Port.  
Use the 'admin' login and the new password that was set previously  
![20](https://github.com/user-attachments/assets/680772b6-63c4-4ffb-9b04-891ce13c8ee0)  
Like this one  
![21](https://github.com/user-attachments/assets/f00aafc2-eeb0-4c82-9678-2e2f87295ba1)  
### Configure MikroTik  
Click on 'Interfaces' and rename ether1 to ether1-Internet and ether2 to ether2-Client  
![21-2](https://github.com/user-attachments/assets/7eb3a0e6-703c-4aab-adad-a181d4eeb241)  
Click on 'IP > Addresses > New'. Set the IP address to 10.0.2.20/24 and set the interface to 'ether1-Internet'  
To get this IP, I created a Windows virtual machine and set its network adapter to NAT.    
![WVM](https://github.com/user-attachments/assets/c5f51c85-2c0a-4055-87ec-b60fb625ad6e)  
As we can see, the Windows virtual machine has the IP 10.0.2.15/24, which is in the same network as 10.0.2.20/24  
![22](https://github.com/user-attachments/assets/6aa0dda5-50a9-457e-8baa-f9bebce51ec8)  
Click 'New' again and set the IP address to be used by the client  
In this case, I set it to 192.168.14.1/24 and set the interface to 'ether2-Client'.  
![23](https://github.com/user-attachments/assets/3499c175-01e7-448b-b034-07887302e2b1)  
Click on 'IP > DNS' and set the DNS servers to 8.8.8.8 and 8.8.4.4 (Google's DNS)  
![24](https://github.com/user-attachments/assets/6e7d39a3-8045-48fb-9c84-23274c09e751)  
Click on 'IP > Routes > New' and add the gateway 10.0.2.2, which is the NAT gateway  
![25](https://github.com/user-attachments/assets/8baefd96-75f4-4a04-bd0c-a10fc6feba9e)  
Click on 'IP > DHCP Server > DHCP Setup', select 'ether2-Client', then click 'Next' until the setup is complete  
![26](https://github.com/user-attachments/assets/1e9efcb5-a58b-4d54-ab50-856c8a242406)  
Click on 'IP > NAT', select 'srcnat' for Chain, and set the Out. Interface to 'ether1-Internet'  
- srcnat (Source NAT) is used to change the source IP address of outgoing packets, typically to allow devices in a private network to access the internet using the router's public IP.  
- Out. Interface refers to the router interface that sends packets out to the external network, such as the internet. For example, if your router connects to the internet via ether1-Internet, you set Out. Interface to ether1-Internet to apply NAT on packets leaving through that interface.  
![27](https://github.com/user-attachments/assets/23a35bda-06c9-4951-8d39-e05d03bf5c0e)  
For Action, select 'masquerade'  
Masquerade is a type of Source NAT that allows devices on a private network to access the internet using the router's public IP address. It changes the source IP of outgoing packets to the router's public IP, making it ideal for networks with dynamic IP addresses.  
![28](https://github.com/user-attachments/assets/e81104f6-d088-4ecb-b170-f69465944c39)  
Change Adapter 2 on the MikroTik VM to 'Internal Network'
We can set the name to 'Mikrotik' (optional).  
![29](https://github.com/user-attachments/assets/dc39ea82-59f3-4996-88dd-22d89ab6d093)  
Change Adapter on the Windows VM to 'Internal Network' and set the name to 'Mikrotik' as well  
![30](https://github.com/user-attachments/assets/a7fe8036-2a62-4fd8-b927-adb8c6d0ac84)  
Check the IP address on the Windows VM. We get the IP 192.168.14.254 (DHCP).  
![31](https://github.com/user-attachments/assets/81e2bde8-58cd-489f-9711-c5821df844ad)  
We can also check 'IP > DHCP Server > Leases' to see which client has received the IP.  
![32](https://github.com/user-attachments/assets/1e0deb10-9f4d-4366-a5e7-5f9d446ea58d)  
Check the ping to the gateway and Google  
![33](https://github.com/user-attachments/assets/02c47b34-a26b-4914-828d-a8acbc2d0fa5)
