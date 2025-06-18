
![microsoft-azure](https://github.com/user-attachments/assets/b0706064-5fed-4587-8418-3a7f0e6fc896) 

<h1>Observing Network Traffic, and Network Security Groups (NSGs)</h1>
We will observe various network traffic to and from Azure VMs using Wireshark, as well as experiment with Network Security Groups.

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

  - Filter ssh in Wireshark
  - Then, over in PowerShell, you will want to type in "ssh" and then your username from your Linux VM, and then right after @ and the private IP. For example, mine was "userlinux@10.0.0.5", then hit enter.

![Azure-Lab Part4a](https://github.com/user-attachments/assets/92097add-355d-4128-be27-4110668db560)

  - You will then notice some information comes up in Wireshark, but not much
  - Let's continue, enter in your password for your Linux VM and then hit enter

![Azure-Lab Part4b](https://github.com/user-attachments/assets/1bd71a8f-df7d-477d-8c62-fb6142b3096b)

  - You can play around in PowerShell with some Linux commands, but when you're done, just type exit
  - Just to note: this connection is secure and encrypted
  - You will notice that a little bit more information will be displayed to you.

![Azure-Lab Part4c](https://github.com/user-attachments/assets/3d7aa04a-3fa9-4971-99d3-5ee8a52681af)

  - Just to note: this next section is extremely tricky. At least for me, it was anyway, so I will do my best to explain my process and dumb it down as best as I can. 
  - Let's filter DHCP in Wireshark
  - Now, over in PowerShell, type in ipconfig /renew and then enter
  - Not a whole lot happened
  - DO NOT type in ipconfig /release because you will crash your VM, and it will literally take what seems like forever for it to be usable again. 

![Azure-Lab Part4d](https://github.com/user-attachments/assets/73c41cfa-45a1-4fab-bccb-ba6e995970d5)

  - Let's create some DHCP Traffic
  - Open a Notepad and type in ipconfig /release, and then under type ipconfig /renew
  - Then File > Save
  - From there, type c:\programdata and then enter and save it into that folder as dhcp.bat as all files. The reason I say to do it that way is because you will not be able to find that folder by going the route of This PC > Windows (C:) > ProgramData because the folder, for lack of a better term, is not visible that way.
  - This is the part where I got hung up on, and hopefully this dumbs it down as best as possible

![Azure-Lab Part4d](https://github.com/user-attachments/assets/22a3e491-12ce-4072-b835-6a9e40a24ef3)

![Azure-Lab Part4e](https://github.com/user-attachments/assets/c516ebd7-fd51-45f3-a24c-ae9fce20962f)

![Azure-Lab Part4f](https://github.com/user-attachments/assets/2991bf8c-a5db-41d8-9787-118911d15cc2)

  - Let's go back to PowerShell now, and type in cd c:\programdata, then enter
  - ls, then enter
  - You'll get a little bit of information, but let's move on
  - Type the file we just created .\dhcp.bat and let's see what happens

![Azure-Lab Part4g](https://github.com/user-attachments/assets/964f8e58-759c-48b3-9665-78dd64f4d308)

  - We will notice that some things will happen here
  - The Windows VM will temporarily stop and then start
  - We will notice that we have created some DHCP traffic in Wireshark

![Azure-Lab Part4h](https://github.com/user-attachments/assets/29807ce2-4784-4d2b-b864-5f27f51a1c19)

<h2>Step 5: Observe DNS & RDP Traffic</h2>

  - We are going to look at DNS Traffic now.
  - Filter DNS in Wireshark
  - In PowerShell, let's look up the IP for Disney.com
  - 130.211.198.204

![Azure-Lab Part5a](https://github.com/user-attachments/assets/44774645-602e-4a24-86c3-f5f1b476900f)

  - Then type 130.211.198.204 in the browser

![Azure-Lab Part5b](https://github.com/user-attachments/assets/5853cd34-ac14-4f2a-b436-1c14ca4fbf61)

  - At least we got a funny animation, which is cool.
  - Something to think about is that the IP address is related to the animation; however, most sites you can't access directly to the site with the IP address. It's because we probably don't have access, or there is a protocol in place with DNS, because DNS translates human-readable language into something the machine can read.

  - Let's move on
  - In Wireshark, type tcp.port == 3389 and enter
  - Look at all the traffic flowing through
  - TCP port 3389 is the RDP
    
![Azure-Lab Part5c](https://github.com/user-attachments/assets/d66aa05a-cfd0-4a88-a965-52bc3fc86645)

  - I am unsure why, maybe it can be explained to me in the future, but when you type RDP in Wireshark, less traffic flows through there
  - I guess that under protocol, there is a label, and maybe the traffic through the remote desktop flows through another label, but I am probably wrong. If you get a hold of me, let me know.

![Azure-Lab Part5d](https://github.com/user-attachments/assets/41adca74-6f1d-47b4-bf4a-6b4495fe48c7)

<h2>Conclusion</h2>

We have completed this lab. We connected to RDP, looked at some different traffic using Wireshark, and we connected to our Linux-VM through Windows using PowerShell. We also created a security rule to deny traffic that is related to the Cyber world. Make sure that you turn your VMs off, both Windows and Linux, or if you are done using them, then go ahead and delete them. As always, thank you for following along, and hopefully, you learned something because I learned a lot. 
