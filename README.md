<h1>Active Directory and Domain Controller Setup</h1>

<h2>Description</h2>
In this video I walkthrough how to create an Active Directory home lab environment, setup a Domain Controller, and connect to it with a client computer using any account you create in the Domain.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Active Directory</b> 
- <b>Oracle VirtualBox</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (Enterprise Edition)
- <b>Windows Server 2022</b>


<h2>Program walk-through:</h2>

<p align="center">
In the Oracle, VM VirtualBox Manager, create A new Virtual Machine and name it DC for Domain Controller, change the version to Other Windows (64-bit) Bit, and click next, increase the Base memory to 2048 MB, and processors to 2 if you can. Click next to finish. Now right-click DC, go to settings, and under Network click on Adapter 2, Click Enable Network Adapter, and under Attached to: change it to Internal Network. Now click OK. <br/>
<img src="https://i.imgur.com/31EGwvf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now double-click your domain controller. Now you can select your correct Windows 2022 ISO file. On the next page, it shows Select the operating system and you need to click on the Standard Evaluation (Desktop Experience) version. Now continue and click Custom: Install, and next. create the password and I will name it Password1 for the sake of the project.   <br/>
<img src="https://i.imgur.com/cO7Bant.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now that it's installed, click Input and use the shortcut (Input,Keyboard,Insert,Ctrl-Alt-Del) to enter the server. <br/>
<img src="https://i.imgur.com/jnmHbuG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
The next thing to do is click on devices at the top and Insert guest additions CD Image. Now click on files, go to this pc, and click on VirtualBox Guest Additions. Now click on VBoxWindowsAdditions-amd64 and click Reboot now.  <br/>
<img src="https://i.imgur.com/VTky2BU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/N6a4bZo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
<br />
<br />
We are going to rename the VM, so right-click on the start at the bottom left, go to system, click Rename this PC, and name it DC. <br/>
<br />
<br />
Once you are back in were going to click on Network and go to Change adapter options.
<br />
<br />
Now right-click on the left side and go to status and details. Now when you see the IPv4 Address that has a lot of numbers such as 169.254.37.134, We are going to rename this as INTERNAL, this network is not connected to the internet. We will name the other network INTERNET. So what we are going to do is right-click and select Properties, select Internet Protocol Version 4. click Use the following IP address 172.16.0.1, the subnet mask is 255.255.255.0 and the Preferred DNS server is 127.0.0.1. Now click OK.
<br /> 
<br />
<img src="https://i.imgur.com/AxXPZe0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now that's done we can add DHCP, active directory, so go to the Server Manager and click Add roles and features. Click next until you get to Server Roles and click DHCP Server, add features, Active Directory Domain Serves, and Remote Access. Now click next until you get to the role services page and add routing. When the installation is finished hit close. 
<br />
<br />
Now at the top with the flag, the first thing we will do is click it and click promote this server to a domain controller. Click Add a new forest and where the root domain name is type in mydomain.com. Click next and the password is Password1. Click next until you click install and close it and it will restart the VM.
<br /> 
<br />
Now we will set up the RAS/NAT. On the top right click on Tools and Routing and remote access. Right-click DC (local) and click Configure and Enable Routing and Remote Access. Click Next, and click Network address translation (NAT). keep it on Use this public interface to connect to the internet, and Finish.  <br/>
<img src="https://i.imgur.com/Yn3SZDp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now we are going to set up the DHCP so go to tools and DHCP, click your domain, and right-click IPv4, New scope. 
<br />
<br />
<img src="https://i.imgur.com/Vqgxuvf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Click next and call it the IP address so 172.16.0.100-200, and next. Now click the start address is 172.16.0.100, the end is 172.16.0.200, and the length would be 24. 
<br />
<br />
<img src="https://i.imgur.com/pKIzMco.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Click next until you get to Router (Default Gateway), make it 172.16.0.1, and click Add, and next until finish. Before it will function we will right-click your mydomain and click authorize. Hit refresh and now your IPv4 should turn green.
<br />
<br />
<img src="https://i.imgur.com/7j2cggi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now we are going to make the Windows 10 client server. Head back to the virtual box but keep DC running. Now click New and name it CLIENT1 and keep the Version Windows 10 (64-bit). Base memory is 2040MB and 2 Processors. 35GB Hard Disk, and Finish.
<img src="https://i.imgur.com/xt6K9FC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/FwBbM1L.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/XaB4cVA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now right-click and go to settings, Go to Network, and under Attached to: change it to Internal Network. Now click ok and start the VM. Now when the ISO Box pops up, you can add the Windows 10 ISO Which is available on this link https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise. Download the 64-bit edition ISO-Enterprise.
<br />
<img src="https://i.imgur.com/SZmsz4y.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now we will let it install. When the screen Which type of installation do you want? Click Custom Install instead of Upgrade, and when the screen Sign in with Microsoft shows up, click Domain Join instead in the bottom left. Where it says Choose privacy settings for your device, turn off all settings, and Cortana help. 
<br />
<img src="https://i.imgur.com/cO7Bant.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/PB8tUE3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now that it's finished setting up and you are logged in go to the command prompt we can type in (ipconfig) to see if we have a Default gateway is the Ip from the domain controller and type in ping google.com and it successfully works and has a 0% loss than everything is working correctly.
<br />
<img src="https://i.imgur.com/kVhKW0F.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
Now we will connect to the domain controller so we can log in with any account in the database. Right-click the start menu go to the system, Rename this PC (advanced).
<img src="https://i.imgur.com/qJATZOE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Click To rename this computer or change its domain or workgroup. click Change. Change the Computer name: to CLIENT1 and Member of Domain: mydomain.com and on Computer Name/Domain Changes put a-yourname and Password1 and click OK.
Now when logging in go to Other user and use your a-yourname and Password1.
