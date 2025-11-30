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

![image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/2.png)

<br/>
<br/>

Now, choose "Active Directory Domain Services" and then click "Add Features." 
<br/>

![image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/3.png)
![image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/4.png)
<br />
<br/>


Select "Active Directory Domain Services," then check "Restart the destination server automatically."
<br/>

![Screenshot 2024-10-03 144834](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/5.png)
<br />
<br/>


Next, we need to promote this machine to a domain controller by setting it up as a new forest named "mydomain.com." To do this, click the flag and caution icon, then select "Promote this server to a domain controller."
<br/>

![image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/6.png)
<br/>
<br/>

Select "Add a new forest," then enter "mydomain.com" in the Root Domain Name field.
<br/>

![image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/7.png)

<br/>
<br/>

Now, enter a password of your choice and click "Next."
<br/>

![Screenshot 2024-10-03 150945](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/8.png)
<br/>
<br/>

Next, leave the "Create DNS delegation" option unchecked. Continue clicking "Next" until the second screen appears, then click "Install." The machine will restart automatically once the installation is complete.
<br/>

![Screenshot 2024-10-12 011412](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/9.png)
![Screenshot 2024-10-03 151524](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/10.png)
<br/>
<br/>

Sign back in using "mydomain.com\labuser" (or the username you created) along with the password you set for the account. "Mydomain.com" is prefixed to the username because this VM has been promoted to a domain controller, requiring the exact domain context for user authentication.
<br/>
  
![Image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/11.png)
<br/>
<br/>

Now, we'll create an admin user. Go to the search bar and select "Active Directory Users and Computers."
<br/>

![Image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/12.png)
<br/>
<br/>

Right-click the "mydomain.com" folder, then under "New," select "Organizational Unit" and name it "_EMPLOYEES." Next, repeat the same steps to create another folder called "_ADMINS."
<br/> 

![Image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/13.png)
<br/>
<br/> 

Next, we'll create a new user in the "_ADMINS" folder. To do this, right-click on the "_ADMINS" folder, select "New," and then choose "User
<br/>

![Image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/14.png)
<br/>
<br/>

During the user creation process, we'll set a password, leave "User must change password at next logon" unchecked, and check "Password never expires" (this is not typically recommended in real life, but we'll do it for the project). 
<br/>

![Image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/15.png)
<br/>
<br/>

Jane Doe has been added to the "_ADMINS" OU, but she hasn't been granted admin privileges yet. To assign her as an admin, right-click her username, select "Properties," go to the "Member of" tab, and click "Add." Type "Domain admins," click "Check names," then click "OK," "Apply," and finally "OK" to confirm.
<br/>

![Image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/16.png)
![Image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/17.png)
<br/>
<br/>

After logging in, we'll access the Client-1 VM. To connect the client to the domain, go to the search bar and navigate to the "System" section, then select "Rename PC (advanced)." Click "Change," choose "Domain," and enter "mydomain.com." Finally, select "OK.
<br/> 

![Image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/18.png)
<br/>
<br/>

Next, it will ask for an account with permissions to join the domain. Enter Jane's credentials in the username and password sections. The machine should try and restart after successfully entering the credentials. 
<br/>

![Image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/19.png)
<br/>
<br/>

After the restart, Client-1 is now a member of the Domain. 
<br/>

![Image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/20.png)
<br/>
<br/>

Finally, we'll create another OU named "_CLIENTS," following the same steps used for "_EMPLOYEES" and "_ADMINS." Then, drag and drop "CLIENT-1" from "Computers" into the "_CLIENTS" folder.
<br/>

![Image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/21.png)
![Image](https://github.com/aaronsethroberson/deploy-active-directory/blob/main/images/22.png)
<br/>
<br/>
