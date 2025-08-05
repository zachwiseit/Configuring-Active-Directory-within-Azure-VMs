<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Cloud-Based Active Directory Deployment (Azure)</h1>
This tutorial guides you through the essential steps to set up Active Directory and deploy it on a Virtual Machine.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell
- Windows App(macOS)

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
- macOS Sonama 14.6.1

<h2>High-Level Deployment Steps</h2>

- Build a Domain Controller and Client Virtual Machines
- Install Active Directory 
- Creating users with Powershell
- Configuring a Group Policy
- Enabling and Disabling Accounts

<h2>Deployment and Configuration Steps</h2>
First things first go to Azure and Log in. 
After that go to resource groups. 
<p>
<p>
<img <img width="1440" alt="ADI_1" src="https://github.com/user-attachments/assets/2d9ac81b-08e8-4e57-ad77-d6ec00d5b3fa" />
</p>
<p>
Give your resource group a name, choose a region, and click next. 
<p>
<img <img width="1440" alt="ADI_2" src="https://github.com/user-attachments/assets/f332f0f2-06a0-4b45-9ba5-87a1b52a8820" />
</p>
<p>
Click "Create". 
<p>
<img <img width="1440" alt="ADI_3" src="https://github.com/user-attachments/assets/9c6eb03b-d612-4233-a67d-810403a1d004" />
</p>
<p>
Once that is created we will create our virtual network. 
<p>
<img <img width="1440" alt="ADI_4" src="https://github.com/user-attachments/assets/0903f103-281f-43e1-8052-326c7ad463a4" />
</p>
<p>
Go to "Virtual Networks". 
<p>
<img <img width="1440" alt="ADI_5" src="https://github.com/user-attachments/assets/681528ed-9d1c-401a-b0bb-4292f890171b" />
</p>
<p>
Click "Create".
<p>
<img <img width="1440" alt="ADI_6" src="https://github.com/user-attachments/assets/02aba210-c9a5-426c-bef8-8d8fb896ba64" />
</p>
<p>
Choose the resource group created earlier and choose a "Virtual network name". 
At the bottom click "Review + create" until you see create at the bottom. 
<p>
<img <img width="1440" alt="ADI_7" src="https://github.com/user-attachments/assets/32715820-3b6f-4b8a-bf3c-cbb550bdaf22" />
</p>
<p>
Click "Create". 
<p>
<img <img width="1440" alt="ADI_8" src="https://github.com/user-attachments/assets/68b06819-aa5b-4dad-88bb-c29f1a622e89" />
</p>
<p>
With our network made next step is to make the virtual machines. 
<p>
<img <img width="1440" alt="ADI_9" src="https://github.com/user-attachments/assets/2997647e-cf92-4cc6-8398-86f9b74bf3fa" />
</p>
<p>
Go to "Virtual Machines".
<p>
<img <img width="1440" alt="ADI_10" src="https://github.com/user-attachments/assets/8a15b73d-db51-475e-9047-4dabbeda996c" />
</p>
<p>
Choose your created resource group and choose your virtual machine name. 
<p>
<img <img width="1440" alt="ADI_11" src="https://github.com/user-attachments/assets/3511107f-93fa-4af1-a4ec-e09b7eda13b7" />
</p>
<p>
Scroll down to "Image" and MAKE SURE you choose Windows Server 2022. If you choose anything else the rest of this will not work.
<p>
<img <img width="1440" alt="ADI_12" src="https://github.com/user-attachments/assets/2d19a02c-27f3-4d2d-bdb1-0eac5528efd5" />
</p>
<p>
For Size choose anything with 2 vcpus. Then choose your Username and password. 
<p>
<img <img width="1440" alt="ADI_13" src="https://github.com/user-attachments/assets/e06a9da6-e91c-45c3-95e9-9f5bc61128d8" />
</p>
<p>
Check both licensing boxes at the bottom and click  "Next : Disks". 
<p>
<img <img width="1440" alt="ADI_15" src="https://github.com/user-attachments/assets/042979a9-c07a-4bcc-9d78-fe7f8ff45fd5" />
</p>
<p>
Click "Next : Networking" 
<p>
<img <img width="1440" alt="ADI_16" src="https://github.com/user-attachments/assets/1da372f5-8d91-48b7-8abc-0e0816c4709a" />
</p>
<p>
For Virtual network choose the network created earlier. Leave the other settings as is and click "Review + Create". 
<p>
<img <img width="1440" alt="ADI_18" src="https://github.com/user-attachments/assets/08136261-00d2-427f-9bea-857f07c84c2f" />
</p>
<p>
Click "Create" at the bottom.
<p>
<img <img width="1440" alt="ADI_19" src="https://github.com/user-attachments/assets/e3bbb399-692b-4e94-bf2e-6b7b38e839e4" />
</p>
<p>
Now that the virtual machine for the Windows server is created we will create another Virtual machine. 
<p>
<img <img width="1440" alt="ADI_20" src="https://github.com/user-attachments/assets/4510d154-91cf-459b-8b77-dc7650c627d9" />
</p>
<p> 
Same as before go to Virtual Machines. 
<p>
<img <img width="1440" alt="ADI_21" src="https://github.com/user-attachments/assets/c0e73362-666c-4e02-8bd8-df42eb7caa30" />
</p>
<p>
Use the same resource group as before and name the VM with something like "client-1". 
Choose the same Region as the other VM. 
<p>
<img <img width="1440" alt="ADI_22" src="https://github.com/user-attachments/assets/0bb080c5-c04d-49f8-9fdc-c023dbfea77c" />
</p>
<p>
For the Image make sure to use Windows 10 Pro. 
Choose a size that has atleast 2 vcpus.
Make a username and password. 
<p>
<img <img width="1440" alt="ADI_24" src="https://github.com/user-attachments/assets/77514393-3058-4890-9476-26b9055b4ec8" />
</p>
<p>
Scroll to the bottom, check the Licensing box, and click "Next : Disk". 
<p>
<img <img width="1440" alt="ADI_25" src="https://github.com/user-attachments/assets/2d737b32-6caf-4c93-972e-5915a334a7c7" />
</p>
<p>
Click "Next : Networking" 
<p>
<img <img width="1440" alt="ADI_26" src="https://github.com/user-attachments/assets/fd1780c3-ab77-4c44-9928-3c47064c8535" />
</p>
<p>
Choose the Vnet you created and click "Review + create". 
<p>
<img <img width="1440" alt="ADI_27" src="https://github.com/user-attachments/assets/d184952d-f549-402e-80a2-105f22280195" />
</p>
<p>
Click "Create". 
<p>
<img <img width="1440" alt="ADI_28" src="https://github.com/user-attachments/assets/72b0ba26-fdc3-4aa0-81f6-f46cc1c73d10" />
</p>
<p>
Next we need set the virtual NIC private IP address to stay static. 
<p>
<img <img width="1440" alt="ADI_29" src="https://github.com/user-attachments/assets/60e5b6d3-8744-4983-a90a-ebf5770c0afd" />
</p>
<p>
In Virtual Machines click on dc-1(the Windows Server VM you created) and click "Network Settings". 
<p>
<img <img width="1440" alt="ADI_30" src="https://github.com/user-attachments/assets/d929619f-9d9f-44db-98e2-1ef44cd72e01" />
</p>
<p>
Click on the Network Interface card at the top. 
<p>
<img <img width="1440" alt="ADI_31" src="https://github.com/user-attachments/assets/e9096db4-9021-4650-8e13-6be14dc7f7c2" />
</p>
<p>
Click "ipconfig1". 
<p>
<img <img width="1440" alt="ADI_32" src="https://github.com/user-attachments/assets/d3794c8b-95a3-4d98-a984-2560a059a0a1" />
</p>
<p>
Under Private IP address settings for Allocations choose Static and click save. 
<p>
<img <img width="1440" alt="ADI_33" src="https://github.com/user-attachments/assets/631da8ea-6f64-4c79-af10-e61ac51332a5" />
</p>
<p>
Next we are going to log into dc-1 and disable the Windows Firewall. 
Go into Virtual machines and copy the Public IP address for dc-1
<p>
<img <img width="1440" alt="ADI_35" src="https://github.com/user-attachments/assets/12515ba7-a482-4392-b7e4-6806b533c385" />
</p>
<p>
For Mac Open up the Window App and click "Add PC". 
<p>
<img <img width="1440" alt="ADI_36" src="https://github.com/user-attachments/assets/b6e048ee-c584-4ebc-86ee-b66a93301055" />
</p>
<p> 
For PC name paste the public IP address, choose a Friendly name, and click "Add".
<p>
<img <img width="1440" alt="ADI_37" src="https://github.com/user-attachments/assets/5cabf939-177c-4773-b1e0-d7d9fb31e564" />
</p>
<p>
With it added click dc-1. 
<p>
<img <img width="1440" alt="ADI_38" src="https://github.com/user-attachments/assets/6278e8d3-1701-46ba-854f-4d215bf78be3" />
</p>
<p>
Put in the credentials for that PC. 
<p>
<img <img width="1440" alt="ADI_39" src="https://github.com/user-attachments/assets/35749e8f-a702-4ff4-a680-77021deccfc3" />
</p>
<p>
Click "Continue".
<p>
<img <img width="1440" alt="ADI_40" src="https://github.com/user-attachments/assets/c576c12f-b435-4793-bee8-51854dc92ce7" />
</p>
<p>
Then your Windows Server will start up. 
<p>
<img <img width="1440" alt="ADI_41" src="https://github.com/user-attachments/assets/ab0cc6e2-5380-4c5b-8c3a-da11a1d2ceb6" />
</p>
<p>
IF you did not create a Windows Server You wont see this Server Manager Dashboard. 
<p>
<img <img width="1440" alt="ADI_42" src="https://github.com/user-attachments/assets/51a0fbcc-e099-41dc-aca8-476272013166" />
</p>
<p>
Here is another way to confirm if it is correct or not. 
Right Click the window and then "System".
<p>
<img <img width="1440" alt="ADI_43" src="https://github.com/user-attachments/assets/509cf590-f935-484c-9754-23dece0e4a21" />
</p>
<p>
In the About section under "Windows Specifications you will see Windows Server 2022 Azure Edition. 
If you don’t see that then unfortunatlty you will have to recreate the vm as a Windows Server. 
<p>
<img <img width="1440" alt="ADI_44" src="https://github.com/user-attachments/assets/7e16f3b7-df00-4d98-ba4f-ad3e5d2865ee" />
</p>
<p>
Next right click the start menu and click "Run". 
<p>
<img <img width="1440" alt="ADI_45" src="https://github.com/user-attachments/assets/9e0c9d32-4a54-498b-8ffc-66a0d3a87716" />
</p>
<p>
Then type wf.msc and click "OK".
<p>
<img <img width="1440" alt="ADI_46" src="https://github.com/user-attachments/assets/4164dec5-ea58-4e76-98d5-8e9b0450f9c0" />
</p>
<p>
This will bring up the Windows Defender Firewall. 
Click "Windows Defender Firewall Properties". 
<p>
<img <img width="1440" alt="ADI_47" src="https://github.com/user-attachments/assets/f36fbaf8-a23f-4b6f-9437-56640f998036" />
</p>
<p>
In the Domain Profile tab for Fire wall state change it from on to off. 
<p>
<img <img width="1440" alt="ADI_48" src="https://github.com/user-attachments/assets/2b5d14f8-0040-42d9-9a33-ac1a486798d1" />
</p>
<p>
Do the same for the Firewall state in Private Profile. 
<p>
<img <img width="1440" alt="ADI_49" src="https://github.com/user-attachments/assets/f0b36908-634a-4298-80de-ff8d8bf4892b" />
</p>
<p>
Then the same for Public Profile as well. 
<p>
<img <img width="1440" alt="ADI_50" src="https://github.com/user-attachments/assets/6dc89ada-d89c-4089-803c-520170667e7e" />
</p>
<p>
Click "Apply" and then "OK". 
<p>
<img <img width="1440" alt="ADI_51" src="https://github.com/user-attachments/assets/8a333735-55be-4391-bec6-a8e2dc710a8d" />
</p>
<p>
Close that page and the Firewall is off. 
<p>
<img <img width="1440" alt="ADI_53" src="https://github.com/user-attachments/assets/2e2d1992-795a-458e-9f63-d0efc04e00f4" />
</p>
<p>
Now we are going to change the DNS settings in Client-1 to point to dc-1's private IP address. 
Go back to Azure and click on "Virtual Machines".
Click on "dc-1" under Overview scroll down to its Private IP address and copy it. 
<p>
<img <img width="1440" alt="ADI_54" src="https://github.com/user-attachments/assets/2ca3f0a5-744d-465f-aa9b-364b07149850" />
</p>
<p>
Now click on "Client-1 and go to Networking then click "Network Settings". 
<p>
<img <img width="1440" alt="ADI_56" src="https://github.com/user-attachments/assets/1b5e80b1-d61c-4daa-bcbb-f7600a7c80a5" />
</p>
<p>
Click on the tab Network Interface.
<p>
<img <img width="1440" alt="ADI_57" src="https://github.com/user-attachments/assets/cd8d893f-1560-4cf6-9207-131f58f35a5c" />
</p>
<p>
On the left click "DNS servers" 
<p>
<img <img width="1440" alt="ADI_58" src="https://github.com/user-attachments/assets/f41becbe-3010-478d-aa64-1c987e1449fb" />
</p>
<p>
It should be set to inherit from virtual network. change that to custom. 
<p>
<img <img width="1440" alt="ADI_59" src="https://github.com/user-attachments/assets/4dba399c-d8a5-4089-8054-db55b0df9d74" />
</p>
<p>
Now paste dc-1 private IP address in the DNS server.
<p>
<img <img width="1440" alt="ADI_60" src="https://github.com/user-attachments/assets/8d534c09-0e38-4efa-8e57-515c69d7f706" />
</p>
<p>
Then click Save at the top. 
<p>
<img <img width="1440" alt="ADI_61" src="https://github.com/user-attachments/assets/bb83dbe2-6d7a-4b4f-ac2f-2c36354cf3c4" />
</p>
<p>
Next we need to restart Client-1 from the Azure portal. 
Click the box next to client-1. 
<p>
<img <img width="1440" alt="ADI_63" src="https://github.com/user-attachments/assets/1bf64d2f-25df-4e50-b353-b3949019e5df" />
</p>
<p>
Click "Restart" at the top right. 
<p>
<img <img width="1440" alt="ADI_64" src="https://github.com/user-attachments/assets/0907894e-0e8e-487d-8f50-afc53f460551" />
</p>
<p>
Click "Yes".
<p>
<img <img width="1440" alt="ADI_65" src="https://github.com/user-attachments/assets/cce2ea40-0235-40e1-a0b3-86b87c22309e" />
</p>
<p>
Now that its restarted we are going to log into client-1 and ping dc-1 private IP address. 
Next we need to add client-1 as a PC and log into it. 
<p>
<img <img width="1440" alt="ADI_66" src="https://github.com/user-attachments/assets/260f3d07-1d0f-4d6a-a3f7-0b791d43117e" />
</p>
<p>
Copy the public IP address for client-1.
<p>
<img <img width="1440" alt="ADI_67" src="https://github.com/user-attachments/assets/40958800-7dcc-489e-a9c5-ea4407af0b43" />
</p>
<p>
Paste it into the PC name, enter a Friendly name and press ADD
<p>
<img <img width="1440" alt="ADI_68" src="https://github.com/user-attachments/assets/b3526750-10a1-4cb5-a724-5cf7e4d7472c" />
</p>
<p>
Enter the client-1's credentials. 
<p>
<img <img width="1440" alt="ADI_69" src="https://github.com/user-attachments/assets/cfd2fc57-fa5b-4d35-838d-b149e8ba6c93" />
</p>
<p>
Click "Continue" 
<p>
<img <img width="1440" alt="ADI_70" src="https://github.com/user-attachments/assets/0cf823e3-bcef-4391-81d5-1f2c7a35f38b" />
</p>
<p>
Select no for everything and click "Accept".
<p>
<img <img width="1440" alt="ADI_71" src="https://github.com/user-attachments/assets/e1e25f61-b03c-47fc-b523-2f1750502d9b" />
</p>
<p>
Now we can attempt to ping dc-1's private IP address but first we need to get it. 
<p>
<img <img width="1440" alt="ADI_72" src="https://github.com/user-attachments/assets/ff26720d-9973-4d2e-924b-8a1036ab8e4c" />
</p>
<p>
Back in Azure under Virtual Machines click "dc-1" and under Overveiw copy the Private IP address. 
<p>
<img <img width="1440" alt="ADI_73" src="https://github.com/user-attachments/assets/6c25f89a-de8f-49f1-98d8-8958f2fe77de" />
</p>
<p>
Back in client-1 in the search bar type in powershell and open "Windows PowerShell". 
<p>
<img <img width="1440" alt="ADI_74" src="https://github.com/user-attachments/assets/7bd51889-534f-4701-9999-dc83d83f4a18" />
</p>
<p>
Next to "labuser>" type ping and paste the private IP address. 
<p>
<img <img width="1440" alt="ADI_77" src="https://github.com/user-attachments/assets/7aa47eff-d730-40e9-bf90-db19772f2688" />
</p>
<p>
Just like this and click enter. 
<p>
<img <img width="1440" alt="ADI_78" src="https://github.com/user-attachments/assets/4acdb159-834d-414f-9a84-f4416abac530" />
</p>
<p>
After you hit Enter it should ping looking like this showing the replies from the IP address
<p>
<img <img width="1440" alt="ADI_79" src="https://github.com/user-attachments/assets/a8aac6ef-7678-46d4-8da9-f2e30a73da0e" />
</p>
<p>
Next in Powershell run ipconfig /all and press enter. The output should show dc-1's private IP address like in this image. 
<p>
<img <img width="1440" alt="ADI_80" src="https://github.com/user-attachments/assets/a5a9aafd-ed76-4388-941f-fda5a8ad7466" />
</p>
<p>
