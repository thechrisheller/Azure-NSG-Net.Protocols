
![microsoft-azure](https://github.com/user-attachments/assets/b0706064-5fed-4587-8418-3a7f0e6fc896) 

<h1>Observing Network Traffic, and Network Security Groups (NSGs)</h1>
We'll observe various network traffic to and from Azure VMs with Wireshark as well as play around with Network Security Groups.

<h2>Prerequisite</h2>

  - [Microsoft Azure Account](https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account/search?ef_id=_k_Cj0KCQjwzYLABhD4ARIsALySuCTvMpKHbOeSo9lv81A8vCg1XGDNwpOIuOsD2o8pmLnyl7dVku-Yn3IaApK-EALw_wcB_k_&OCID=AIDcmmfq865whp_SEM__k_Cj0KCQjwzYLABhD4ARIsALySuCTvMpKHbOeSo9lv81A8vCg1XGDNwpOIuOsD2o8pmLnyl7dVku-Yn3IaApK-EALw_wcB_k_&gad_source=1&gbraid=0AAAAADcJh_uVoYZIZMJRJFQ3v8k-BGmp2&gclid=Cj0KCQjwzYLABhD4ARIsALySuCTvMpKHbOeSo9lv81A8vCg1XGDNwpOIuOsD2o8pmLnyl7dVku-Yn3IaApK-EALw_wcB)
  - [Creating VM in the Cloud](https://github.com/thechrisheller/Creating-VM-Azure/tree/main)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Remote Desktop
- Powershell
- SSH, RDH, DNS, HTTP/S, ICMP
- Wireshark

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)
- Linux Ubuntu

<h2>Steps</h2>

  - Step 1: Connect to VM using RDP & Install Wireshark
  - Step 2: Observe ICMP Traffic
  - Step 3: Use NSG (Firewall) to deny ping
  - Step 4: Observe SSH & DHCP Traffic
  - Step 5: Observe DNS & RDP Traffic

<h2>Steps on Actions, Inspecting, and Observations</h2>

<h2>Step 1: Connect to VM using RDP & Install Wireshark</h2>
  - Make sure that your Windows and Linux VMs are running
  - If they are not, turn them on

![Azure-Lab Part1a](https://github.com/user-attachments/assets/18e1ceb0-d988-43a9-910e-4e35073d8141)

  - Copy your Public IP Address from your Windows VM
  - Then go to your Remote Desktop, paste the IP address you just copied into it

![Azure-Lab Part1b](https://github.com/user-attachments/assets/e928f8ec-053e-4460-af80-1a753f78f5de)

![Azure-Lab Part1c](https://github.com/user-attachments/assets/34588b8e-41b0-4ddd-9e4e-01623d47388d)

  - Enter your Windows username and password that you created for your Windows VM

![Azure-Lab Part1d](https://github.com/user-attachments/assets/7e5c20d3-018e-4572-8b19-10e01beba93a)

  - Once you're all set up inside the VM, go to the web browser and type in www.wireshark.org and click download
  - From there, select Window x64 Installer

![Azure-Lab Part1e](https://github.com/user-attachments/assets/1176db82-a1b7-4e19-a3d3-74ca84cdc4b4)

![Azure-Lab Part1f](https://github.com/user-attachments/assets/af531754-85bf-4e38-a30b-0661839bf88f)


<h2>Step 2: Observe ICMP Traffic</h2>

  - Open Wireshark and select where it says "Ethernet"
  - Once you do that, you'll notice the shark fin will turn blue in the upper left-hand corner, and select it.

![Azure-Lab Part2a](https://github.com/user-attachments/assets/e41913bb-081b-4274-964f-3b6b9349467c)

  - You will now see a bunch of traffic flowing through the network

![Azure-Lab Part2b](https://github.com/user-attachments/assets/adbb630f-460a-4cf9-8baa-d0429550d03f)

  - At the filter bar above, type "icmp" and "enter"
  - Notice the traffic is gone
  - We are now just filtering the icmp traffic

![Azure-Lab Part2c](https://github.com/user-attachments/assets/61d43960-37ee-4bf9-b15d-555dd2b0e6ad)

  - Now lets go back and get the private IP Address from the linux machine we created

![Azure-Lab Part2d](https://github.com/user-attachments/assets/a6938161-9be1-4143-95e1-13772c9d9ffb)

  - Back into the VM on Windows and open PowerShell as an admin from your Windows search bar

![Azure-Lab Part2e](https://github.com/user-attachments/assets/721fb11a-11d2-4e06-b849-f0ebbaa13ca9)

  - From PowerShell, type "ping 10.0.0.5" or whatever the private address is in your VM
  - Notice in Wireshark what happens

![Azure-Lab Part2f](https://github.com/user-attachments/assets/b26168ea-5bc0-4717-ac2d-83df4325432a)

  - Because the icmp filter is on in Wireshark, we are only seeing icmp traffic over the network. This filter allows us to see our Windows-VM (10.0.0.4) send the request to the Linux-VM (10.0.0.5), and the Linux-VM sends a reply back to the Windows-VM. Wireshark and PowerShell both show that we just successfully tested the connection between the two VMs!
 - In PowerShell, initiate a perpetual ping to the Linux-VM with the command ping 10.0.0.5 -t. This command tells the Windows-VM to ping the Linux-VM nonstop

![part 2 final](https://github.com/user-attachments/assets/89dfc540-2dd2-4c94-a653-2376f84c2441)

<h2>Step 3: Use NSG (Firewall) to deny ping</h2>

  - Head back to Azure and go to your Linux VM settings
  - Go to Network Settings
  - Inbound security rules
  - Select the Network Security Group

![Azure-Lab Part3a](https://github.com/user-attachments/assets/86c91386-502a-4a69-a339-26079a662f66)

  - +Add
  - Action: Deny
  - Priority: 290
  - Select "Add"

![Azure-Lab Part3b](https://github.com/user-attachments/assets/6e65f8c0-a312-4b0b-b0ae-05a821538b23)

  - Notice we have added an Inbound security rule

![Azure-Lab Part3c](https://github.com/user-attachments/assets/a3f21ee7-2d3e-454d-bbbe-7706a375875b)

  - Go back to Powershell and Wireshark and what happened

![Azure-Lab Part3d](https://github.com/user-attachments/assets/3490a0d7-8413-4594-b0a4-c2dac7eeb845)

  - The ping request starts to time out in PowerShell because of the new rule we created in the Network Security Group.
  - We can see exactly when the rule took effect and started to deny the ping request from the Windows-VM in Wireshark.
  - Notice when the reply and request change to just a request. 

![Azure-Lab Part3e](https://github.com/user-attachments/assets/bce654f5-470b-4706-bbb3-9a99364c2702)

  - We can delete this rule, and we have completed this part of the lab

![Azure-Lab Part3f](https://github.com/user-attachments/assets/b08947bf-e553-4dd4-9a79-bfab2dbb9eda)

  - Before moving to the next part in PowerShell and do "CTRL + C" to stop the repeating of the Linux scan.

<h2>Step 4: Observe SSH & DHCP Traffic</h2>

