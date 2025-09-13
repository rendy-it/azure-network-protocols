<p align="center">
<img width="2560" height="1440" alt="Header " src="https://github.com/user-attachments/assets/38f28b95-91f5-4c75-96b1-2f34aee53912" />
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
This tutorial demonstrates the methods of observing various network traffics to and from the Azure Cloud infrastructure’s virtual machines with Wireshark, as well as experiment with Network Security Groups.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Windows and Linux Virtual Machines on Microsoft Azure
- Remote Desktop Connection
- PowerShell and numerous Command-Line Tools
- Multiple Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Packet analyzer or Network sniffer)


<h2>Operating Systems Used </h2>

- Windows 10 Pro (21H2)
- Linux Ubuntu Server (24.04) 

<h2>High-Level Steps</h2>

-	Step 1: Connect to the VM using RDP. Within the VM, install Wireshark
- Step 2: Observe ICMP Traffic 
- Step 3: Configure a Firewall (NSG: Network Security Group)  
- Step 4: Observe SSH Traffic
- Step 5: Observe DHCP Traffic
- Step 6: Observe DNS Traffic
- Step 7: Observe RDP Traffic

  

<h2>Steps in Executing, Observing and Inspecting</h2>
<h2> << Step 1: Connect to VM using RDP and Install Wireshark >> </h2>
<p>
<img width="1351" height="394" alt="Step 1" src="https://github.com/user-attachments/assets/9a468935-ef0c-41f0-abca-5f849e58558e" />

</p>
<p>
  
- On the Virtual Machines page of your Azure Resource Group, make sure that both the Windows and Linux virtual machines have a status of “Running”.

</p>
<br />

<img width="1126" height="391" alt="Step 1a" src="https://github.com/user-attachments/assets/f58eb304-f16e-4107-8b77-ada8a87988aa" />

<p>
  
- Click on your Windows VM.
- On the page of your Windows VM:		
  - Copy the “Public IP address” number.

  
</p>
<br />

<img width="338" height="210" alt="Step 1b" src="https://github.com/user-attachments/assets/6b9c3942-8f6a-4fe5-bfa6-4217deb82e7c" /> <img width="88" height="210" alt="Right Pointing Arrow for Step 1b" src="https://github.com/user-attachments/assets/057bcdc6-657b-4729-8145-5e76b138e218" /> <img width="343" height="235" alt="Step 1b1" src="https://github.com/user-attachments/assets/c435dd5c-2240-40df-b03f-94e04ce06b83" />


</p>
<p>
  
- Open the Remote Desktop App:
  - Paste the Windows VM ip address that you copied. Then click on Connect.
  - Then, enter the Windows VM username and password that you created and click on Ok to login.


</p>
<br />

<p>
<img width="1415" height="776" alt="Step 1c" src="https://github.com/user-attachments/assets/7d62e908-70f6-49ed-b82a-b9dfe4c90242" />

</p>
<p>
  
- Once inside the VM:
  - Go to the web browser.
  - Go to www.wireshark.org.
  - Click on “Download Now”.
  
</p>
<br />
<p>
<img width="1391" height="721" alt="Step 1d" src="https://github.com/user-attachments/assets/9af8b2f7-3ad4-4205-9548-1b9d0abc571b" />


</p>
<p>
  
- Select the “Windows x64 Installer”.
 
</p>
<br />
<p>
<img width="1188" height="894" alt="Step 1e" src="https://github.com/user-attachments/assets/7377b6b2-cd74-4a07-8789-76d567ee99fc" />

</p>
<p>
  
- Once Downloaded, click and open the installer to install Wireshark.

</p>
<br />

<h2> << Step 2: Observe ICMP (Internet Control Message Protocol) Traffic >> </h2>

<p>
<img width="887" height="735" alt="Step 2a" src="https://github.com/user-attachments/assets/4d8c0aba-fa8f-4ddb-8c8f-d238ac864b95" />

</p>
<p>
  
- Open Wireshark:
  - Click on “Ethernet”.
  - Then click on the small blue shark fin icon that is at the top left corner.
  - This will initiate a packet capture. 


</p>
<br />

<img width="973" height="529" alt="Step 2b" src="https://github.com/user-attachments/assets/7ebace2b-a739-4781-87bd-e0c4a2921225" />

<p>
  
- Once you do that, you will see various network traffic flows occurring.
   
</p>
<br />

<p>
<img width="689" height="303" alt="Step 2c" src="https://github.com/user-attachments/assets/aca34aa7-c4fd-410d-af56-0453b25d4beb" />


</p>
<p>
  
- At the “Apply a Display filter” bar at the top:
  - Type “icmp” and press enter.
  - All the of traffic flows will disappear. Because it will now only show traffic that is pinged.


</p>
<br />

<p>
<img width="667" height="241" alt="Step 2d" src="https://github.com/user-attachments/assets/cceb643f-f595-477a-ab68-9f2a732a92a1" />


</p>
<p>
  
- Next, minimize the windows VM, go back to your Azure VMs web page to get the Linux VM private ip address.
   - You will find it under the Networking section of your VM's properties tab.
   
</p>
<br />
<p>
<img width="748" height="616" alt="Step 2e" src="https://github.com/user-attachments/assets/2796a37d-ccbf-47a6-ad72-eab71a168d63" />

</p>
<p>

- Next, go back to the Windows VM, go to the windows search bar, search for “PowerShell”.
  - Once you find it open PowerShell as an administrator.

</p>
<br />
<p>
<img width="538" height="268" alt="Step 2f" src="https://github.com/user-attachments/assets/ffc7780c-4adc-4917-8369-ab8d91b38847" />

</p>
<p>

- Once in PowerShell type “ping” then type or paste your Linux private ip number.
  - Example: ping 10.1.0.5 


</p>
<br />
<p>
<img width="592" height="395" alt="Step 2g" src="https://github.com/user-attachments/assets/d5979511-5fb3-4127-84dc-9eda418faa11" />


</p>
<p>

- Next, PowerShell will display the ping statistics of the packets sent by the Linux VM and the packets received by the Windows VM.


</p>
<br />
<p>
<img width="969" height="355" alt="Step 2h" src="https://github.com/user-attachments/assets/af1b77ed-aed8-4761-acab-dbbb2cc65ddc" />


</p>
<p>
  
- Once you ping, Wireshark will capture and display its icmp traffic flow. 
  - Will display ping requests from the Windows VM (10.1.0.4) and replies from the Linux VM (10.1.0.5) within the Wireshark interface.

  
</p>
<br />
<p>
<img width="906" height="555" alt="Step 2j" src="https://github.com/user-attachments/assets/6bcdbe06-270b-4f2e-9e41-58029cdb5857" />

</p>
<p>
  
- Then you will be able to see the VM that you just created with all the information.
  
</p>
<br />
<h2> << Step 3: Create a Linux Virtual Machine within Azure >> </h2>

<p>
<img width="643" height="595" alt="Step 3" src="https://github.com/user-attachments/assets/887a00b4-561a-4e1c-a6e4-ed3434c42aa8" />

</p>
<p>
  
- Repeat the same step process as you did in Step 2:
  - Select the same resource group as the Windows VM.
  - Give the VM a name.
  - Select a Zone.
  - Select “Ubuntu Server 24.04 LTS – x64 Gen2”.



</p>
<br />
<p>
<img width="674" height="491" alt="Step 3a" src="https://github.com/user-attachments/assets/41b9416c-1ec1-4a42-bb96-1a6f57134131" />


</p>
<p>
  
- For the memory size, keep it the same as the Windows VM.
- Next, check the “Password” box for “Authentication type”.
- Next, create a Username and Password.


</p>
<br />
<p>
<img width="645" height="815" alt="Step 3b" src="https://github.com/user-attachments/assets/98b50ea7-43c9-4079-9b63-774136dfe81d" />

</p>
<p>
  
- Then go to the “Networking” tab
- Make sure to select the same Virtual Network as the Windows VM.
- Keep everything else default and select “Review + create”


</p>
<br />
<p><img width="309" height="450" alt="Step 3c" src="https://github.com/user-attachments/assets/d45fc70e-8462-4f28-9b27-90c141e54950" /> <img width="88" height="442" alt="Arrow-Pointing-Right for Step 3c" src="https://github.com/user-attachments/assets/4818d701-1d71-4125-ad02-8b2d8f4ad061" /> <img width="315" height="450" alt="Step 3c1" src="https://github.com/user-attachments/assets/f0a912da-d814-4187-adc9-09db46f5e08c" />

</p>
<p>
  
- On the next Page:
  - Double Check to make sure everything is to your liking.
  - Then select “Create”.

</p>
<br />
<p>
<img width="383" height="407" alt="Step 3d" src="https://github.com/user-attachments/assets/2ac1e6f2-5449-4bd3-bcdc-bb0ff0db0852" />

</p>
<p>
  
- Just like Step 2, deployment will take a couple of minutes, so be patient.
- Once completed you can click on “Go to resource”. 

  
</p>
<br />
<p>
<img width="1189" height="715" alt="Step 3e" src="https://github.com/user-attachments/assets/66fc8e83-ad65-4536-9f66-64000cf578d8" />

</p>
<p>
  
- Then you will be able to see the VM that you just created with all the information.

</p>
<br />
<h2> << Conclusion >> </h2>

<p>
<img width="1409" height="685" alt="Step 3f" src="https://github.com/user-attachments/assets/52648836-e25e-47ae-a0b2-46df78c29910" />

</p>
<p>
  
- Go Back to your resource group page.
- There you will be able to see all that you have created so far.
  - A Windows 10 Virtual Machine.
  - A Linux Virtual Machine.

</p>
<br />
<p>
<img width="1360" height="405" alt="Step 3g" src="https://github.com/user-attachments/assets/841c623c-a846-4ae9-8778-3620105db576" />



</p>
<p>
  
- Also, make sure your VMs are on “Stop” status if you are not going to use them right away. This way you will not be charged while they are not in use.
- To conclude, we have successfully created both a Windows and Linux Virtual Machine inside of the Microsoft Azure cloud infrastructure.


</p>
<br />
