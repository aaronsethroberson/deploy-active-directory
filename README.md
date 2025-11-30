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
<br/>
<br/>

If it's not already visible, we'll launch Server Manager on our Domain Controller.
<br/>
<br/>


![Screenshot 2024-10-03 144451](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/1.png)
<br/>
<br/>

Next, we'll select "Add roles and features." When we reach the "Select destination server" window, we'll click "Server Selection" and ensure that "Select a server from the server pool" is checked. There should be only one available option in the server pool. 
<br/> 

![image](https://github.com/user-attachments/assets/15114d9b-418b-424e-a074-1e6c5453fd1c)

<br/>
<br/>

Now, choose "Active Directory Domain Services" and then click "Add Features." 
<br/>

![image](https://github.com/user-attachments/assets/6cb06787-0bbd-4e78-93ab-9af7df5c67b2)
![image](https://github.com/user-attachments/assets/1cfaddab-9bbd-4c35-babc-5be8e8c76f73)
<br />
<br/>


Select "Active Directory Domain Services," then check "Restart the destination server automatically."
<br/>

![Screenshot 2024-10-03 144834](https://github.com/user-attachments/assets/d371cad7-da41-4df9-ba44-71955e5f72bb)
<br />
<br/>


Next, we need to promote this machine to a domain controller by setting it up as a new forest named "mydomain.com." To do this, click the flag and caution icon, then select "Promote this server to a domain controller."
<br/>

![image](https://github.com/user-attachments/assets/84d57430-93ca-44c6-81fd-2e176fa6911f)
<br/>
<br/>

Select "Add a new forest," then enter "mydomain.com" in the Root Domain Name field.
<br/>

![image](https://github.com/user-attachments/assets/870becb2-82dc-4f2e-9605-1e418449d73a)

<br/>
<br/>

Now, enter a password of your choice and click "Next."
<br/>

![Screenshot 2024-10-03 150945](https://github.com/user-attachments/assets/51e1b5c9-71c9-4782-919a-cf5ad5685c9b)
<br/>
<br/>

Next, leave the "Create DNS delegation" option unchecked. Continue clicking "Next" until the second screen appears, then click "Install." The machine will restart automatically once the installation is complete.
<br/>

![Screenshot 2024-10-12 011412](https://github.com/user-attachments/assets/9eea97dc-259c-4b2a-b1d0-70d304b0ad8d)
![Screenshot 2024-10-03 151524](https://github.com/user-attachments/assets/0a38db2e-8f66-4059-9e42-907c41cf0409)
<br/>
<br/>

Sign back in using "mydomain.com\labuser" (or the username you created) along with the password you set for the account. "Mydomain.com" is prefixed to the username because this VM has been promoted to a domain controller, requiring the exact domain context for user authentication.
<br/>
  
![Image](https://github.com/user-attachments/assets/c275f379-14ed-4e3b-980a-8d80e90ad0f7)
<br/>
<br/>

Now, we'll create an admin user. Go to the search bar and select "Active Directory Users and Computers."
<br/>

![Image](https://github.com/user-attachments/assets/b764ce6f-ed2b-4a3a-85ad-0ee8d764aaee)
<br/>
<br/>

Right-click the "mydomain.com" folder, then under "New," select "Organizational Unit" and name it "_EMPLOYEES." Next, repeat the same steps to create another folder called "_ADMINS."
<br/> 

![Image](https://github.com/user-attachments/assets/57bf0f36-fab4-43be-ad66-e69d93a0ea23)
<br/>
<br/> 

Next, we'll create a new user in the "_ADMINS" folder. To do this, right-click on the "_ADMINS" folder, select "New," and then choose "User
<br/>

![Image](https://github.com/user-attachments/assets/c8ac368a-93d6-429f-acf5-9ec781f664ca)
<br/>
<br/>

During the user creation process, we'll set a password, leave "User must change password at next logon" unchecked, and check "Password never expires" (this is not typically recommended in real life, but we'll do it for the project). 
<br/>

![Image](https://github.com/user-attachments/assets/b05b95a6-5a02-4851-9dac-643e110dd9ac)
<br/>
<br/>

Jane Doe has been added to the "_ADMINS" OU, but she hasn't been granted admin privileges yet. To assign her as an admin, right-click her username, select "Properties," go to the "Member of" tab, and click "Add." Type "Domain admins," click "Check names," then click "OK," "Apply," and finally "OK" to confirm.
<br/>

![Image](https://github.com/user-attachments/assets/695f6be0-129e-4797-ac0f-48311bb9acc3)
![Image](https://github.com/user-attachments/assets/7478efd5-e45f-4e84-a545-12efd368322f)
<br/>
<br/>

After logging in, we'll access the Client-1 VM. To connect the client to the domain, go to the search bar and navigate to the "System" section, then select "Rename PC (advanced)." Click "Change," choose "Domain," and enter "mydomain.com." Finally, select "OK.
<br/> 

![Image](https://github.com/user-attachments/assets/b3616301-3237-4cb3-a42e-06f6a3c88870)
<br/>
<br/>

Next, it will ask for an account with permissions to join the domain. Enter Jane's credentials in the username and password sections. The machine should try and restart after successfully entering the credentials. 
<br/>

![Image](https://github.com/user-attachments/assets/cb43663e-46f1-488a-b713-2267714442a5)
<br/>
<br/>

After the restart, Client-1 is now a member of the Domain. 
<br/>

![Image](https://github.com/user-attachments/assets/94cca414-cadb-4723-88c4-45974a161a2c)
<br/>
<br/>

Finally, we'll create another OU named "_CLIENTS," following the same steps used for "_EMPLOYEES" and "_ADMINS." Then, drag and drop "CLIENT-1" from "Computers" into the "_CLIENTS" folder.
<br/>

![Image](https://github.com/user-attachments/assets/f6227402-63f9-487a-8495-e696ec454ab9)
![Image](https://github.com/user-attachments/assets/b821f678-3336-49c3-92fc-340f479baf1a)
<br/>
<br/>
