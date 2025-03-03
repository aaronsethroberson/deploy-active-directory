<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Deploying Active Directory in Azure</h1>
In this section of Active Directory, we will install Active Directory on the Domain Controller, set up a domain client, and join the client to the domain within the Virtual Machine<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure 
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 
- Windows 10 


<h2>Project Walkthrough</h2>

<p align="center">
If its not already displayed, we are going to launch Server Manager on our Domain Controller
<br/>

![Screenshot 2024-10-03 144451](https://github.com/user-attachments/assets/63cd699f-2067-4e01-bcf5-b8a98e010aec)

<br/>

<p align="center">
Next we're going to select "Add roles and features". Once we arrive at the "Select destination server" window, we will click "Server Selection" and then we will make sure "Select a server from the server pool" is checked. There should only be one option to choose in the server pool. 
<br/> 

![image](https://github.com/user-attachments/assets/15114d9b-418b-424e-a074-1e6c5453fd1c)

<br/>


<p align="center">
Now select "Active Directory Domain Services" then select "Add features": 
<br/>

![image](https://github.com/user-attachments/assets/6cb06787-0bbd-4e78-93ab-9af7df5c67b2)
![image](https://github.com/user-attachments/assets/1cfaddab-9bbd-4c35-babc-5be8e8c76f73)

<br />

<p align="center">
Select Active Directory Domain Services". Now select "Restart the destination server automatically":
<br/>

![Screenshot 2024-10-03 144834](https://github.com/user-attachments/assets/d371cad7-da41-4df9-ba44-71955e5f72bb)

<br />

<p align="center"> 
Next, we need to promote this machine to a domain controller by configuring it as a new forest with the name "mydomain.com." To do this, click on the flag and caution icon, then choose "Promote this server to a domain controller.
<br/>

![image](https://github.com/user-attachments/assets/84d57430-93ca-44c6-81fd-2e176fa6911f)

<p align="center">
Select "Add a new forest" and next we're going to type: "mydomain.com" into the Root Domain name section. 
<br/>

![image](https://github.com/user-attachments/assets/870becb2-82dc-4f2e-9605-1e418449d73a)

<br/>

<p align="center">
Now we're going to enter a password of our choosing and then select "Next"
<br/>

![Screenshot 2024-10-03 150945](https://github.com/user-attachments/assets/51e1b5c9-71c9-4782-919a-cf5ad5685c9b)

<br/>

<p align="center">
Next, we'll leave the "Create DNS delegation" option unchecked. Continue clicking "Next" until the second screen appears, then select "Install." The machine will automatically restart after the installation is complete
<br/>

![Screenshot 2024-10-12 011412](https://github.com/user-attachments/assets/9eea97dc-259c-4b2a-b1d0-70d304b0ad8d)
![Screenshot 2024-10-03 151524](https://github.com/user-attachments/assets/0a38db2e-8f66-4059-9e42-907c41cf0409)

<br/>

<p align="center">
Sign back in using "mydomain.com\labuser" (or the username you created) along with the password you set for that account. The "mydomain.com" is added before the username because this VM has been promoted to a domain controller, and it needs to know the exact domain context of the user you're signing in as
<br/>
  
![image](https://github.com/user-attachments/assets/e2637f23-2a2e-4ed7-9b98-1710d36e16e4)

<br/>

<p align="center">
Now we will create an admin user. Navigate to the search bar and select "Active Directory Users and Computers" 
<br/>

![Screenshot 2024-10-03 153728](https://github.com/user-attachments/assets/f4551d58-6246-4b15-ba54-8f9026c60de4)

<br/>

<p align="center">
Right-click on the "mydomain.com" folder, then under "New," select "Organizational Unit" and name it "_EMPLOYEES." Next, repeat the same steps to create another folder named "_ADMINS". 
<br/> 

![Screenshot 2024-10-03 153925](https://github.com/user-attachments/assets/16f3fbc8-f141-4cb2-b0a5-7536a3f126dc)
![Screenshot 2024-10-03 160200](https://github.com/user-attachments/assets/91fda991-2885-452c-8c25-2547b0f371a4)

<br/> 

<p align="center"> 
Next, we'll create a new user in the "_ADMINS" folder. To do this, right-click on the "_ADMINS" folder, select "New," and then choose "User
<br/>

![Screenshot 2024-10-03 154322](https://github.com/user-attachments/assets/32a37eff-a2e7-4237-a81d-fec7c012693c)

<br/>

<p align="center"> 
In the process of creating the User we will need to create a password and leave "User must change passsword at next logon" unchecked and "Password never expires" checked (Probably wouldn't do this in real-life, but we will for the project. 
<br/>

![Screenshot 2024-10-03 154530](https://github.com/user-attachments/assets/62ed4f68-1d1a-409d-b1b2-957397510598)

<br/>

<p align="center">
Jane Doe has been added to the "_ADMINS" OU, but she hasn't been officially assigned as an admin yet. To finalize her admin status, right-click on her username, select "Properties," go to the "Member of" tab, and click "Add." Type "Domain admins," click "Check names," then hit "OK," "Apply," and "OK" again to confirm.
<br/>

![Screenshot 2024-10-03 160643](https://github.com/user-attachments/assets/d8a9b38f-6810-4a05-ba18-81b2534e346c)
![Screenshot 2024-10-03 160600](https://github.com/user-attachments/assets/b243013b-dc00-40c3-9d9b-20ae0e71cd78)

<br/>

<p align="center"> 
Now we will log out of the DC and log back in as Jane using her credentials 
<br/>

![Screenshot 2024-10-03 155343](https://github.com/user-attachments/assets/6589a3b6-0e06-4efe-a175-876968be6ae5)

<br/> 

<p align="center"> 
After logging in, we'll access the Client-1 VM. To connect the client to the domain, go to the search bar and navigate to the "System" section, then select "Rename PC (advanced)." Click "Change," choose "Domain," and enter "mydomain.com." Finally, select "OK.
<br/> 

![Screenshot 2024-10-03 162736](https://github.com/user-attachments/assets/bcda3555-8d0a-4a74-9a0f-a886ec1242c9)

<br/>

<p align="center"> 
Next it will as for an account with permissions to join the domain. Enter Jane's credentials in the username and password sections. The machine should try and restart after successfully entering the credentials. 
<br/>

![Screenshot 2024-10-03 162927](https://github.com/user-attachments/assets/3d90a4bf-d6fe-44c8-842f-1cda6cd7e489)

<br/>

<p align="center">
After the restart, Client-1 is now a member of the Domain. 
<br/>

![Screenshot 2024-10-03 163145](https://github.com/user-attachments/assets/3e2c7163-4287-42c5-9e45-691c7397f017)

<br/>

<p align="center"> 
Lastly we will create another OU titled "_CLIENTS" with same steps we used before with "_EMPLOYEES" and "_ADMINS". Drag and drop "CLIENT-1" from "Computers " into the "_CLIENTS" folder. 
<br/>

![Screenshot 2024-10-03 163304](https://github.com/user-attachments/assets/7585d3e5-baf6-477f-b759-b2c85390443a)
![image](https://github.com/user-attachments/assets/0b4ac92f-e90e-40f1-92a9-81907c6d42ec)
