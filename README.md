
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
