# osTicket-Lab-Tutorial-1

## osTicket Lab & Tutorial 1: Azure Cloud Configuration and Installation

![osticket thumb png 6b3b5efa4e131f26aa85e446c89e0591](https://user-images.githubusercontent.com/114452968/231029106-6d310402-66e5-4e00-8e3f-83ff30c0b2de.png)

For the purpose of this lab, we will assume you know how to access Microsoft Azure for the purposes of starting up a Virtual Machine. If you need help setting up the basics of Azure please refer to my Active Directory Lab here: https://github.com/husselltech/AzureADLab

Make sure you create a Resource Group and your Virtual Machine needs to have a minimum of 4 (four) CPU’s. I will be running Windows 10 Pro version 21H2. Once the Virtual Machine is deployed, in Azure find and copy the public IPv4 address of your VM. From your Windows search bar find your Remote Desktop Connection app and connect to your VM.

During this lab you will need various referenced installation files which can be found here: 
https://drive.google.com/drive/u/0/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6
I recommend you open Microsoft Edge on your VM and copy/paste the link.

## Let us begin!

Our first task in our Virtual Machine will be to install/enable IIS (Internet Information Services). Go to Control Panel > Programs > Turn Windows features on or off > [X] Internet Information Services > [X] World Wide Web Services > [X] Application Development Features > [X] CGI. This setting allows us to have more control over osTicket and use scripts. Click close after Windows completed the requested changes, and then close all open windows.
 
![image](https://user-images.githubusercontent.com/114452968/230914154-01e98250-f0b0-4e90-ae32-2f4582dca3e7.png)

Now it is time to start downloading our installation files from the previously linked Google Drive folder.
 
![image](https://user-images.githubusercontent.com/114452968/230914259-d2af1a3c-3c8b-4639-978d-cc03f3469fb0.png)

Download and install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi). Download and install the rewrite module (rewrite_amd64_en-US.msi).

Next, create a folder in your directory called PHP with the path C:\PHP
 
![image](https://user-images.githubusercontent.com/114452968/230914317-c06e2f4a-a656-4675-9858-f914d10596e2.png)

Download and install PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) and extract the file into the newly made C:\PHP folder.

Download and install the VC_redist.x86.exe file. This is a C++ file.

Download and install MySQL > Typical setup > Launch configuration wizard after install > Standard configuration > Install as a Windows Service > Set a root password (REMEMBER FOR LATER)
 
![image](https://user-images.githubusercontent.com/114452968/230914638-125f9893-238f-425c-bb1b-fa811be94a1d.png)
![image](https://user-images.githubusercontent.com/114452968/230914662-93556168-2958-494f-a4e2-dce96b01b3f9.png)
![image](https://user-images.githubusercontent.com/114452968/230914722-1e4e8bdc-2802-4b13-8238-33e76e67e8f3.png)
![image](https://user-images.githubusercontent.com/114452968/230914737-18e0d8d8-1bf8-4c45-989f-1c2fa73ddb92.png)
![image](https://user-images.githubusercontent.com/114452968/230914766-85808954-496e-46f1-bcef-a6df8b308e57.png)

## IIS: Internet Information Services
 
Our next step is to start up Internet Information Services. Go to the Windows search bar and search for “Internet Information Services” and right click to run as an administrator.
 
![image](https://user-images.githubusercontent.com/114452968/230914901-2d66ae18-a80e-484f-a79d-7303aef1ba80.png)

Open PHP manager and click Register new PHP version. Click the three dots to browse to your C:\PHP folder. Select php-cgi and click Open, then click OK.

![image](https://user-images.githubusercontent.com/114452968/230915104-5d95e2cc-f5ba-4bb7-838b-84435c7dd350.png)
 
Navigate back to the IIS home screen and on the right-hand side under Actions click stop, and then start the server again. Clicking Restart also works.

Back in Microsoft Edge Download the osTicket files: osTicket v1.15.8. Extract ONLY the folder called “upload” and copy it to the folder c:\inetpub\wwwroot; there will be other items in the folder. Once the folder is copied rename “upload” to “osTicket.”
 
![image](https://user-images.githubusercontent.com/114452968/230915164-17a06db7-55b7-48a3-87bc-4319ea8cab0b.png)
![image](https://user-images.githubusercontent.com/114452968/230915195-96e56f53-3e4a-4c19-ad27-acae32181524.png)

Reopen IIS and restart the server. On the left side of IIS click Sites > Default Web Site> osTicket. Then, on the right side of IIS click browse *.80.
 
![image](https://user-images.githubusercontent.com/114452968/230915271-c0acf7f5-9052-45f9-ae6e-f3da988f463d.png)

The osTicket installer will be on the screen and you will see that some of the extensions have not yet been enabled. Leave the screen open and navigate back to IIS. Go to Sites > Default Web Site > osTicket, and select PHP manager. Click enable or disable an extension. Here we are going to enable three extensions, right click and select enable for each one: Php_imap.dll, Php_intl.dll, Php_opcache.dll. Refresh Edge and the changes should be on the screen.

![image](https://user-images.githubusercontent.com/114452968/230915354-1aff3e9f-1111-4ded-bae1-b77f0caf954f.png)
![image](https://user-images.githubusercontent.com/114452968/230915391-44ae062a-b799-433a-9649-931c631a8d41.png)

From Windows File Explorer navigate to C:\inetpub\wwwroot\osTicket\include. Find “ost-sampleconfig.php” and change the name to “ost-config.php.”
 
![image](https://user-images.githubusercontent.com/114452968/230915449-e159bc5d-e674-4a94-a50e-9b7eb398f79c.png)

## Permissions

Now it is time to assign permissions. After renaming right click > Properties > Security > Advanced. Click Disable inheritance > Remove all inherited permissions from this object.
 
![image](https://user-images.githubusercontent.com/114452968/230915510-313d2ac5-a25f-4920-972f-3073f71afbd5.png)

Click add > select a principal > in the text box type “everyone” > Full control > OK > Apply > OK. Exit these screens after completion.
 
![image](https://user-images.githubusercontent.com/114452968/230915857-361480d7-0ae3-4710-a527-f63b418b7f3f.png)
![image](https://user-images.githubusercontent.com/114452968/230915654-824ebd5f-adf3-4e7e-a25b-479cd762551b.png)

In Microsoft Edge at the osTicket Installer click continue. Fill out the System Settings and Admin User Sections. It might be helpful to make a note of names and passwords for later. Stop here for now, and do not do any more this with page until later. Minimize if necessary.
 
![image](https://user-images.githubusercontent.com/114452968/230916025-699de024-eba5-4480-a280-f21ab0501fa8.png)

## SQL

From the installation files download and install HeidiSQL. Follow all the prompts and click Finish. 
 
![image](https://user-images.githubusercontent.com/114452968/230916171-0074ea7f-cf81-4e7c-84bb-eaa25561b985.png)

Open HeidiSQL and click new to create a new session. Keep the username root and put in your password that you created earlier. Remember? Create and name the database osTicket.
 
![image](https://user-images.githubusercontent.com/114452968/230916209-ab3b3a5d-e7f7-41f8-8a32-998b862fbe76.png)
![image](https://user-images.githubusercontent.com/114452968/230916238-3227923f-9c1a-4c9d-b882-008e003dccc7.png)
![image](https://user-images.githubusercontent.com/114452968/230916274-26edbc2a-7d21-4841-a5b2-d431578f8596.png)

 

Go back to the osTicket installer in Microsoft Edge and finish filling out the Database Settings.

-Database: osTicket

-Mysql Username: root

-Mysql Password: whatever you chose

-Click Install Now

You should now be able to log in to your osTicket account here:  http://localhost/osTicket/scp/login.php

End Users can fill out a ticket here: http://localhost/osTicket/
 
 

Finally, we will clean up some files. Go ahead and delete C:\inetpub\wwwroot\osTicket\setup. Change permissions on C:\inetpub\wwwroot\osTicket\include\ost-config.php to read only.

## Summary

We have set up all the necessary tools to begin using the osTicket software. osTicket is an open-source helpdesk suite with a variety of features. This lab consisted of the following technologies: Microsoft Azure Cloud/Virtual Machines, Remote Desktop, Internet Information Services, PHP, SQL, C++, and osTicket. In the next lab/tutorial we will configure osTicket for a SOHO setting.
