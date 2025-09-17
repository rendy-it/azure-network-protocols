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

<h2> << Step 3: Configure a Firewall (NSG: Network Security Group) >> </h2>

<p>
<img width="1415" height="990" alt="Step 3" src="https://github.com/user-attachments/assets/0a2adf23-450a-41d0-8ebb-f217976337ae" />

</p>
<p>
  
- Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM.
  - In PowerShell, type the command “ping 10.1.05 -t”
  - The command makes the Windows VM ping the Linux VM nonstop.


</p>
<br />
<p>
<img width="1654" height="491" alt="Step 3a" src="https://github.com/user-attachments/assets/b19c82b3-f0d7-43d8-8dff-0afd2e4f6e56" />


</p>
<p>
  
- Head back to the VM page of your Azure Resource Group and select your Linux VM.
  - Go to the “Network Settings” page which can be found under the “Networking” tab.
  -	Click on the “Network security group” link which will take you to the “Linux-VM-nsg”.


</p>
<br />
<p>
<img width="885" height="739" alt="Step 3b" src="https://github.com/user-attachments/assets/dec98a50-727d-478f-88f0-05423c558a2e" />

</p>
<p>
  
- Go to the settings tab:
  -	Click on “Inbound security rules” then click on “+Add”. 



</p>
<br />
<p>
<img width="409" height="891" alt="Step 3c" src="https://github.com/user-attachments/assets/1ba31c98-f9d5-491c-bad7-fb4ac751428f" />

</p>
<p>
  
- Next:
  - Select "ICMPv4” for Protocol.
  -	Select “Deny” for Action.
  -	Type in “290” for the Priority box.
  -	Then click on “Add”.


</p>
<br />
<p>
<img width="1594" height="297" alt="Step 3d" src="https://github.com/user-attachments/assets/3d47fd83-f1ff-4631-b95a-b884cb9f7400" />


</p>
<p>
  
- We now have configured a rule that will deny incoming icmp traffic from any source to any destination for the Linux-VM.  

  
</p>
<br />
<p>
<img width="1716" height="939" alt="Step 3e" src="https://github.com/user-attachments/assets/94e5b7f9-d261-491f-a73d-adb1f055233a" />


</p>
<p>
  
- Once you go back to the Windows VM. You will now see that all network traffic requests have been timed out in both PowerShell and Wireshark.

</p>
<br />
<p>
<img width="350" height="395" alt="Step 3f" src="https://github.com/user-attachments/assets/55303eba-beb5-4162-a547-a63ecaef9951" />


</p>
<p>
  
- Next, you can now delete the rule from your Linux-VM.
- Once deleted, the traffic flow will resume.
  
</p>
<br />
<p>
<img width="1555" height="598" alt="Step 3g" src="https://github.com/user-attachments/assets/6e4b28c6-d8e6-487f-9baa-df5a851f11a6" />



</p>
<p>
  
- To stop the network traffic flow, go back to PowerShell and hit “CTRL +C” on your keyboard.   

  
</p>
<br />








<h2> << Step 4: Observe SSH (Secure Shell) Traffic >> </h2>

<p>
<img width="957" height="315" alt="Step 4" src="https://github.com/user-attachments/assets/4fce0dcb-9f13-451c-90a0-fb67593d28ea" />


</p>
<p>
  
- Go Back to the Windows-VM. Have both Wireshark and PowerShell opened.
  - On Wireshark, start a packet capture by following the early steps of Steps 2.
  -	At the “Apply a Display filter” bar at the top.
  -	Type “ssh” and press enter.



</p>
<br />
<p>
<img width="650" height="198" alt="Step 4a" src="https://github.com/user-attachments/assets/f3d46c1a-d86b-45c8-b613-4bf894e8a036" />



</p>
<p>
  
- Then head over to PowerShell.
  - Type ssh, then the username for your Linux VM, then type “@” and then the private ip number. Then hit enter. 
  - Example: username@<private IP address>.
  - Mine is “rendylab@10.1.0.5”.



</p>
<br />
<p>
<img width="751" height="304" alt="Step 4a" src="https://github.com/user-attachments/assets/305d0ac5-672f-43b2-b073-f80079954c92" />



</p>
<p>
  
- Then, type in the password for your Linux-VM account and hit enter.
  - You may not see what you are typing when you type your password in but rest assured it is being typed.



</p>
<br />
<p>
<img width="827" height="871" alt="Step 4b" src="https://github.com/user-attachments/assets/e516d2c3-de02-4ca2-a79c-fab3316d3dab" />



</p>
<p>
  
- Once the command is successful, inside of PowerShell, it will be as if you are connected inside of the Linux-VM command prompt.



</p>
<br />
<p>
<img width="1146" height="766" alt="Step 4c" src="https://github.com/user-attachments/assets/10b14489-afc2-4d5a-80d6-4b6ea978695d" />



</p>
<p>
  
- You are able to experiment with plenty of Linux commands of your choosing.
- Once you are done and satisfied, type exit.

  
</p>
<br />
<p>
<img width="1716" height="939" alt="Step 3e" src="https://github.com/user-attachments/assets/94e5b7f9-d261-491f-a73d-adb1f055233a" />


</p>
<p>
  
- Once you go back to the Windows VM. You will now see that all network traffic requests have been timed out in both PowerShell and Wireshark.

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
