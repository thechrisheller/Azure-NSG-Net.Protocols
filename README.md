
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

  - Once you're all set up inside the VM, go to the web browser and type in www.wireshark.com and click download
  - From there, select Window x64 Installer

![Azure-Lab Part1e](https://github.com/user-attachments/assets/1176db82-a1b7-4e19-a3d3-74ca84cdc4b4)

![Azure-Lab Part1f](https://github.com/user-attachments/assets/af531754-85bf-4e38-a30b-0661839bf88f)

  - It will have you install IMAP as well go ahead and do so

<h2>Step 2: Observe ICMP Traffic</h2>

