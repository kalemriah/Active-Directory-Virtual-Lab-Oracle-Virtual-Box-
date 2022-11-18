
<h1>Active Directory Virtual Lab</h1>


<h2>Description</h2>
This project consists of creating a virtual active directory lab to learn the basics & further knowledge of active diretories. Most companies & schools use active directory networks because it's a very powerful network application with great orgnization & security tools. Creating an AD (Active Directory) virtual lab is a great way to learn the basics of AD & how basic microsft servers work in general.
<br />

<h2> Minimum PC Requirments </h2> 
-8GB+ RAM. I personally reccomend this amount of RAM beaucse I tried to do this lab on my laptop that only had 4GB of RAM and it just wasnt cutting it with the VM often crashing. I upgraded to 16GB RAM to allocate the RAM to the virtual enviorments and it ran smoothly. 

<h2>Languages & Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Virtual Box Oracle</b>

<h2>Environments Used </h2>

- <b>Windows 10 2019 Server</b>
- <b>Windows 10 Desktop</b>
- <b>Virtual box Oracle</b> 

<h2>Lab walk-through:</h2>

<p align="center">
<b>Step 1.) Installation </b>
<p align="left">
 -Install Virtual Box Oracle, https://www.virtualbox.org <br/>
 -Install Windows 10 2019 Server ISO x64, https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019 <br/>
 -Install Windows 10 Desktop ISO x64, https://www.microsoft.com/en-us/software-download/windows10 <br/>
<p align="center">
<b>Step 2.) Create Win10 Server 2019 Virtual Enviorments</b>
<p align="left">
 -Using the Virtual Box 'Tools' select 'New' & create the new VM. Name your new VM "Domain Controller", select next (you will add the ISO file later). Adjust your CPU cores and Memory accordingly (as reccomended above 4GB+ memory is reccomended). Once VM is created, go to the setting of the VM and opent the 'Network' tab. Add a new network adaptor. Under 'Attched to' selecet 'Internal network' and name the network adaptor "Internal". <br/>
 -Start DC VM, select the Win10 2019 server ISO, Install. Once complete, select 'Windows server 2019 desktop experience', 'Custom install', 'Disk 0', and finally allow the VM to complete the installation. <br/> 
 -Once installation is comeplete, create User and Password.
<p align="center">
<b>Step 3.) Installing Vbox Guest Edition for Performance </b>
<p align="left">
 -This step is to increase VM performance <br/>
 -With the DC VM open click the 'devices' tab on the VM toolbar. click 'Guests edititon'. Open the File Explorer on the DC, go to 'This PC', click the 'CD drive Vbox' and then run 'AMD 64' install and then shut down VM and start again.<br/>
<p align="center">
<b>Step 4.) Setting up internal NIC IP Adress in DC VM  </b>
<p align="left">
 -Open 'netowork & internet settings' &rarr; 'Ethernet' &rarr; 'Change adaptor options' <br/>
 -There will be 2 ethernets, idenify which one is connected to the internet & which one is an internal NIC. <br/>
 -Check properties on both *STOPED HERE*
<p align="center">
<b>Step 5.) Installing Active Directory Domain Services & Create Domain</b>
<p align="left">
<p align="center">
<b>Step 6.) Create Domain Admin Account </b>
<p align="left">
<p align="center">
<b>Step 7.) Install Remote Access Server/NAT(Network Adress Translation)</b>
<p align="left">
<p align="center">
<b>Step 8.) Set-Up DHCP on Domain Controller</b>
<p align="left">
<p align="center">
<b>Step 9.) Grab Github Powershell script </b>
<p align="left">
<p align="center">
<b>Step 10.) Create Win10 Client Virtual Enviorment</b>
<p align="left">


</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
