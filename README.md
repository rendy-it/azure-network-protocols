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
<img width="1351" height="394" alt="Step 1" src="https://github.com/user-attachments/assets/b472a94f-237c-40af-bba7-235dd7e06acb" />

</p>
<p>
  
- On the Virtual Machines page of your Azure Resource Group, make sure that both the Windows and Linux virtual machines have a status of “Running”.

</p>
<br />

<p><img width="1126" height="391" alt="Step 1a" src="https://github.com/user-attachments/assets/3c2fc1cd-7b2d-42b4-bf32-5e6eeeb8f4cd" />

<p>
  
- Click on your Windows VM.
- On the page of your Windows VM:		
  - Copy the “Public IP address” number.

  
</p>
<br />

<p><img width="338" height="210" alt="Step 1b" src="https://github.com/user-attachments/assets/f7f2adfd-977a-46f9-b21d-3e9b3bb90ad2" /> <img width="88" height="210" alt="Right Pointing Arrow for Step 1b" src="https://github.com/user-attachments/assets/c6a362d6-6e14-4e6f-ace6-fd674109a7e8" /> <img width="343" height="235" alt="Step 1b1" src="https://github.com/user-attachments/assets/77f06005-fb1c-41eb-bdd5-0e107fc3bb20" />





</p>
<p>
  
- Open the Remote Desktop App:
  - Paste the Windows VM ip address that you copied. Then click on Connect.
  - Then, enter the Windows VM username and password that you created and click on Ok to login.


</p>
<br />

<p>
<img width="1415" height="776" alt="Step 1c" src="https://github.com/user-attachments/assets/2d33530e-3ac4-4dc7-b109-1ec92f573263" />

</p>
<p>
  
- Once inside the VM:
  - Go to the web browser.
  - Go to www.wireshark.org.
  - Click on “Download Now”.
  
</p>
<br />
<p>
<img width="1391" height="721" alt="Step 1d" src="https://github.com/user-attachments/assets/2743908a-b103-46c6-9420-532158d595c4" />


</p>
<p>
  
- Select the “Windows x64 Installer”.
 
</p>
<br />
<p>
<img width="1391" height="721" alt="Step 1d" src="https://github.com/user-attachments/assets/2743908a-b103-46c6-9420-532158d595c4" />


</p>
<p>
  
- Once Downloaded, click and open the installer to install Wireshark.

</p>
<br />

<h2> << Step 2: Create a Windows 10 Virtual Machine within Azure >> </h2>

<p>
<img width="366" height="430" alt="Step 2" src="https://github.com/user-attachments/assets/267b85c2-3469-4ae4-9987-fa30ca81901a" /> <img width="88" height="430" alt="Arrow-Pointing-Right" src="https://github.com/user-attachments/assets/45bfd18c-04b9-43ec-97eb-fee73f38c146" /> <img width="283" height="430" alt="Step 2a" src="https://github.com/user-attachments/assets/240fcf46-aef5-4da9-aae0-95aca704f553" />

</p>
<p>
  
- On the Azure home page, hover you mouse cursor on “Virtual Machines”. 
  - A small window will appear, then click on “Create”.
  - Then select “Virtual Machine” 


</p>
<br />

<p>
<img width="580" height="701" alt="Step 2b" src="https://github.com/user-attachments/assets/4ba29e83-782a-4bd0-8d37-3d4a90663989" />

<p>
  
- On the next page, select the resource group that we created in Step 1.
  - Give the VM a name.
  - Select a Zone
  - Select “Windows 10 Pro” for the OS image.
    - Click on “See all images” to search for it, if you can’t find it.
  - And select at least 2 vcpus, with 8 or 16 gig memory
    - Click on “See all sizes” to search for it, if you can’t find it.
   
  
</p>
<br />

<p>
<img width="692" height="384" alt="Step 2c" src="https://github.com/user-attachments/assets/f7044866-727f-49ed-b3fe-de4ea2a3a487" />

</p>
<p>
  
- Next, create a Username and Password.

</p>
<br />

<p>
<img width="355" height="402" alt="Step 2d" src="https://github.com/user-attachments/assets/c7a8852e-036a-41c1-ab3a-c5442e06b2a9" /> 

</p>
<p>
  
- Next, go back up and click on the “Networking” tab.
   
</p>
<br />
<p>
<img width="548" height="402" alt="Step 2e" src="https://github.com/user-attachments/assets/278ba11d-16f4-4902-aa64-c79d17cd1fe0" />


</p>
<p>

- On the next page:
  - Create a new name for the “Virtual network” box.
  - You will need that same virtual network for the Linux Virtual machine.
  - Everything else is set by default.
</p>
<br />
<p>
<img width="518" height="213" alt="Step 2f" src="https://github.com/user-attachments/assets/3e1d9a16-318f-4dfb-b451-6b34fd4d274f" />
</p>
<p>

- Go back to the “Basics” tab. 
- Scroll to the bottom and check the Licensing checkbox to confirm.
- Then select “Review + Create”.

</p>
<br />
<p>
<img width="336" height="266" alt="Step 2g" src="https://github.com/user-attachments/assets/87223c89-d6b7-40e8-a7fd-63733f2aad11" /> <img width="88" height="266" alt="Arrow-Pointing-Right for Step 2g" src="https://github.com/user-attachments/assets/56f4a4a0-919b-4b9b-8fda-1c7de3a359ab" /> <img width="336" height="266" alt="Step 2g1" src="https://github.com/user-attachments/assets/49586aa9-c625-45df-a11e-86d8f3955cb1" />

</p>
<p>

- On the next Page:
  -	Double Check to make sure everything is to your liking.
  -	Then select “Create”.


</p>
<br />
<p>
<img width="349" height="370" alt="Step 2h" src="https://github.com/user-attachments/assets/aff3ecd9-2639-4a03-918d-b86275aa8944" /> <img width="88" height="370" alt="Arrow-Pointing-Right for Step 2hi" src="https://github.com/user-attachments/assets/b5bbeb1f-0059-4fc0-95fa-d12109050b76" /> <img width="344" height="370" alt="Step 2i" src="https://github.com/user-attachments/assets/23d6a757-ebb3-45a1-83d8-914cab48ab51" />



</p>
<p>
  
- Deployment will take a couple of minutes to complete, so be patient.
- Once completed you can click on “Go to resource”. 
  
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
