
<h1>Active Directory Virtual Lab (Oracle Virtual Box)</h1>


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
 -Check properties on both, the one that is Internal will have autoconfig IPv4 '169.254.196.79', rename the ethernets 'Internet' & 'Internal' for Identification.<br/>
 -Go to properties on 'Internal" NIC, open 'IPv4 (TCP/ID) Properties'<br/>
 -IP adresss = 172.16.0.1 &rarr; Subnet mask = 255.255.255.0 &rarr; Gateway = empty &rarr; DNS = 127.0.0.1 (Loopback Adress)<br/>
 -Finally, right click start menu &rarr; 'system' &rarr; 'rename this pc', name it "DC" &rarr; restart VM<br/>
<p align="center">
<b>Step 5.) Installing Active Directory Domain Services & Create Domain</b>
<p align="left">
-Open 'server manager' app &rarr; on 'Dashboard' open 'Step 2, add roles & features', click 'next' untill 'server selection' tab, select 2019 win server, click 'next', select 'active directrory domain servies' role, click 'next' untill install & install.<br/>
-Once installed, open notifcation flag on toolbar for server manager, under 'post deployment configure' click 'promote this PC'<br/>
-In deployment configuration' select 'add new forest' & name root domain "mydomain.com"<br/>
-Next, create password, continue clicking 'next' untill installed, will automatically restart VM.<br/>
-Login
<p align="left">
<p align="center">
<b>Step 6.) Create Domain Admin Account </b>
<p align="left">
-Windows 'Start' &rarr; 'Windows Administative Tools' &rarr; 'Active Directory Users & Computers'<br/>
-Right click 'mydomain.com' &rarr; 'new' &rarr; 'orginizational unit' <br/>
-Name "ADMINS" &rarr; right click 'ADMINS' &rarr; 'new' &rarr; 'user', create user with your name and password, check 'password never expires' (for the sake of the lab) <br/>
-Right click your user &rarr; 'properties' &rarr; 'member of' &rarr; 'add' &rarr; type "domain admins", click 'check names', click 'okay'<br/>
-Sign out, select 'other user', user admin login just created<br/>
<p align="center">
<b>Step 7.) Install Remote Access Server/NAT(Network Adress Translation)</b>
<p align="left">
-on 'Server manager' app select 'roles & features' &rarr; 'next' &rarr; 'next' &rarr; select server &rarr; select 'remote access' role, select 'routing' box, select next and install<br/>
-On server manager toolbar select 'tools' &rarr; 'routing & remote access', right click 'DC(local)' &rarr; 'configure & enable & remote access', select next, select 'network adress translation(NAT)' &rarr; select the network intergace previously labled "internet" &rarr; finish<br/>
<p align="center">
<b>Step 8.) Set-Up DHCP on Domain Controller</b>
<p align="left">
-Server amanger &rarr; add roles &rarr; next &rarr; select server &rarr; select 'DHCP' roles &rarr; next & install<br/>
-Select 'tools' on server manager taskbar &rarr; select 'DHCP', open 'dc.mydomain.com', right click 'IPv4' &rarr; select 'new scope'<br/>
-Name after scope IP range "172.16.0.100-200", next start IP = 172.16.0.100 &rarr; end IP = 172.16.0.200 &rarr; subnet lenght = 24 &rarr; subnet = 255.255.255.0, click next, use lease date of one day. Select 'yes I want to setup a DHCP controller', click next, enter "172.16.0.1" (DC NAT IP)  for IP, click 'add' , click next, click next & finish<br/>
-Right click 'dc.mydomain.com' & refresh, then the 'IPv4', 'IPv6' icons should be green<br/>
-To allow internet access from DC without "are you sure". Pop-ups config &rarr; select 'off' for 'users' &rarr; select okay (this is done only for the sake of the lab)<br/>
<p align="center">
<b>Step 9.) Grab Github Powershell script to create a ton of users </b>
<p align="left">
-https://github.com/joshmadakor1/AD_PS This is the link is the PowerShell script for creating a ton of users. Install to deskstop or somewhere easily found.<br/>
-Open foler downloaded &rarr; 'names' &rarr; add your name to the top of the file, then save & close.<br/>
-Select windows start &rarr; Windows Powershell &rarr; Powershell ISE &rarr; run as admin.<br/>
-Select folder icon & open Github powershell script<br/>
-Type "Set-ExecutionPolicy Unrestricted" &rarr; change directory of powershell to github file, "C:\User\*admin user name*\desktop\AD-PS-master' select the green play icon to run script<br/> 
<p align="center">
<b>Step 10.) Create Win10 Client Virtual Enviorment</b>
<p align="left">
-Create new VM instance using Oracle virtual machine.<br/>
-Adjust CPU & Memory to PC usage, Name "client"<br/>
-Once created go to settings &rarr; network, change the 'attached to' to 'internal network' &rarr; okay<br/>
-Start Vbox & select win10 ISO &rarr; Install &rarr; select 'win10 Pro' &rarr; next &rarr; select custom, then select Drive 0 &rarr; next & install.<br/>
-Select limited versions & continue without internet &rarr; continue with win10 setup.<br/>
-Once on desktop, open command terminal and type 'Ipconfig' to test the connection to the DC<br/>
-Right click 'windows start' &rarr; 'system', scroll down to 'rename this PC(advance)' &rarr; click 'change', name "client1", select 'member of' domain & type "mydomain.com" &rarr; enter user & password <br/>
-At this point the tutorial is complete and you can now play around and experiment in your active directory!


</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
