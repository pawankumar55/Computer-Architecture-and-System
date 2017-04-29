##Introduction

#Virtual machine

A virtual machine is a software computer that, like a physical computer, runs an operating system and applications. The virtual machine is comprised of a set of specification and configuration files and is backed by the physical resources of a host.

###Configuration and deployment of the virtual machine

The first screen asks for name and operating systems

#Enter 

  Name:ubuntu-1  
  Type:Linex  
  Version: Ubuntu(32)  
  Then Next
  
From the next screen select memory size 512MB.  
From the next screen select "Create a virtual hard drive now"and then select create.  
Then select VDI(virtualbox disk image) and then press next.  
Choose  "Dynamically allocated" and click next.  
Change the size to 10GB. Click Create.  
Now you will see the virtual machine created but in state " powered off".  

#Inserting a virtual cd..  

before starting a virtual machine, click on setting button.  
Click on storage..
You should see :  
-Controller: IDE    
-Empty (with a cd icon)  
-Controller: SATA  
-ubuntu-1.vdi  

Click on CD icon by Empaty. To the right you will see:  
-Attributes  
-CD/DVD DRives: IDE Secondary Master, and another cd icon  
click on this CD icon. From the menu which appears, select"choose a virtual CD/DVD disk file.."  
Browse to the directory where you copied the ubuntu server ISO image, and select it.  
you should now see:  
-Controller: IDE  
-ubuntu- 12.04-3-server -i386  
-Controller: SATA  
-Ubuntu-1.vdi  

click ok.  

#Start the Virtual Machine  

Select the virtual machineand click the green start arrow - or double click the virtual machine and your virtual machine will start.  
The ubuntu installer should start. Click inside the window. Note that you may have to press the host key to get your mouse out again.  
Select your language and press F3 if you want to select a non -US keyboard layout.  
Next press F4 and select" Install a minimal virtual machine".  
Then select " Install Ubuntu Server" from the front menu.  
We do strongly suggest the following settings:  

-Encrypt your home directory? No  
-Partitioning method: Guided - Use entire disk  
-Select none for HTTP proxy  
-No automatic updates  
-Then choose software to install, move to Open SSH Server and hit space to select it, but leave every thing else unselected.  
-Install GRUB boot loader to the master boot record? Yes  
#Restart



