# Install Active Directory

## Step 1: Change the Server Name  
Type **"name"** in the Windows search bar.

![Change Windows Name](/images/change_windows_name.png)


## Step 2: Rename the Server  
Select **"Rename this PC"** and enter the desired server name.  

![Rename PC](/images/rename_pc.png)


## Step 3: Restart the Server  
After renaming, restart the server to apply changes.  

![Restart the Server](/images/restart_the_server.png)


## Step 4: Open "Add Roles and Features"  
Once the server restarts, open **Server Manager**, select **Manage**, and then click **"Add Roles and Features"**.  

![Add Roles and Features](/images/add_roles_and_features.png)


## Step 5: Select "Next"  
Click **Next** on the wizard introduction screen.  

![Select Next - Step 1](/images/select_next01.png)


## Step 6: Select "Next" Again  
Click **Next** to continue through the wizard.  

![Select Next - Step 2](/images/select_next02.png)


## Step 7: One More "Next"  
Click **Next** to proceed to the next configuration step.  

![Select Next - Step 3](/images/select_next03.png)

# Install Active Directory (Continued)

## Step 8: Select "Active Directory Domain Services"
Choose **Active Directory Domain Services** from the list.  

![Active Directory Domain Services](/images/ad_ds.png)


## Step 9: Add Features
When prompted, click **Add Features**.  

![Add Features](/images/add_features.png)


## Step 10: Continue Through the Wizard
Click **Next**.  

![Select Next - Step 4](/images/select_next04.png)  

Click **Next** again.  

![Select Next - Step 5](/images/select_next05.png)  

Click **Next** once more.  

![Select Next - Step 6](/images/select_next06.png)


## Step 11: Allow Restart if Needed
Check **Restart the destination server automatically if required** and click **Yes**.  

![Restart if Needed Box](/images/restart_if_needed_box.png)


## Step 12: Install the Role
Click **Install** to begin the installation process.  

![Install](/images/install.png)  

It may take a few minutes.  

![Installation in Progress](/images/minutes.png)

## Step 13: Promote Server to Domain Controller
After installation completes, select **Promote this server to a domain controller**.  

![Promote to Domain Controller](/images/promote.png)

## Step 14: Add a New Forest
Check **Add a new forest**, type in the **Root domain name**, then click **Next**.  

![New Forest](/images/new_forest.png)

## Step 15: Set the Directory Services Restore Mode (DSRM) Password
Enter a password (can be the same as the original VM admin password).  

![Password](/images/password.png)


## Step 16: Continue Through the Wizard
Click **Next**.  

![Select Next - Step 7](/images/select_next07.png)  

After a few seconds, the NetBIOS domain name will auto-populate. Click **Next**.  

![NetBIOS](/images/NetBIOS.png)  

Click **Next**.  

![Select Next - Step 8](/images/select_next08.png)  

Click **Next** again.  

![Select Next - Step 9](/images/select_next09.png)


## Step 17: Install After Prerequisites Check
Once the prerequisites check completes, click **Install**.  

![Prerequisites Check](/images/prerequisites.png)


## Step 18: Close and Restart
After installation finishes, click **Close** before the server restarts.  

![Restart](/images/restarts.png)


# Configure Certificate Services

## Step 19: Sign Back In
After the restart, log in as an administrator.  

![Admin Sign In](/images/02_domain_join_Admin.png)

# Configure Active Directory Certificate Services

## Step 20: Open Add Roles and Features
After signing in, go back to **Manage** and select **Add Roles and Features**.  

![Add Roles](/images/add_roles.png)

## Step 21: Continue Through the Wizard
Click **Next**.  

![Select Next - Step 10](/images/select_next10.png)  

Click **Next** again.  

![Select Next - Step 11](/images/select_next11.png)  

Click **Next** once more.  

![Select Next - Step 12](/images/select_next12.png)

## Step 22: Select Active Directory Certificate Services
Check **Active Directory Certificate Services**.  

![Active Directory Certificate Services](/images/ad_cs.png)  

After a few moments, click **Add Features** (when prompted).  

![Add Features](/images/ad_features.png)

## Step 23: Continue Through the Wizard
Click **Next**.  

![Select Next - Step 13](/images/select_next13.png)  

Click **Next** again.  

![Select Next - Step 14](/images/select_next14.png)  

Click **Next**.  

![Select Next - Step 15](/images/select_next15.png)  

Click **Next** again.  

![Select Next - Step 16](/images/select_next16.png)

## Step 24: Allow Restart if Required
Check **Restart the destination server automatically if required**, then click **Yes**.  

![Restart if Required](/images/required_box.png)

## Step 25: Install the Role
Click **Install**.  

![Install AD CS](/images/install_ad_cs.png)

## Step 26: Configure Active Directory Certificate Services
After installation, click **Configure Active Directory Certificate Services on the destination server**.  

![Configure AD CS](/images/ad_css.png)  

Click **Next**.  

![Select Next - Step 17](/images/select_next17.png)

## Step 27: Select Certificate Authority
Check **Certificate Authority**, then click **Next**.  

![Certificate Authority](/images/authority.png)

## Step 28: Choose Enterprise CA
Ensure **Enterprise CA** is selected, then click **Next**.  

![Enterprise CA](/images/enterprise_ca.png)  

Click **Next**.  

![Select Next - Step 18](/images/select_next18.png)  

Click **Next** again.  

![Select Next - Step 19](/images/select_next19.png)

## Step 29: Keep Default Cryptography Settings
Keep the default **SHA256** highlighted and click **Next**.  

![SHA256](/images/SHA256.png)

## Step 30: Keep Default CA Settings
Keep the default options selected and click **Next**.  

![Defaults](/images/defaults.png)

## Step 31: Specify Validity Period
Select **5 years** and click **Next**.  

![5 Years](/images/five_yrs.png)

## Step 32: Specify Database Location
Click **Next** to accept the default database location.  

![Database Location](/images/dblocation.png)

## Step 33: Configure AD CS
Click **Configure**.  

![AD CS Configuration](/images/ad_cs_con.png)  

Once configuration is complete and you receive the **"Configuration succeeded"** message, reboot the server.  

![Configuration Succeeded](/images/congratulations.png)

# Setting Network Connections

## Step 34: Open Network Settings
Right-click the network icon in the system tray and select **Open Network & Internet settings**.  

![Network Settings](/images/network.png)

## Step 35: Choose Ethernet
Click **Ethernet**.  

![Ethernet](/images/ethernet.png)

## Step 36: Edit IP Assignment
Click **Edit IP Assignment**.  

![IP Assignment](/images/IP_assignement.png)

## Step 37: Set IP Configuration
Enter the following values as needed for your network.  

![IP Configuration](/images/selections.png)

## Step 38: Verify Network Configuration
Open **Command Prompt** and type:  

```bash
ipconfig /all

You should now see the correct IP address, Gateway, and DNS.