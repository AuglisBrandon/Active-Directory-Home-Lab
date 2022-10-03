<h1>Active Directory Home Lab</h1>

 

<h2>Description</h2>
Project consists of how to setup a Basic Home Lab running Active Directory (AD) using Orcale Virtual Box while also adding users with Powershell.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Powershell<b>
- <b>Acitve Directory<b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)
- <b>Windows Server 2019</b> 
- <b>Oracle Virtualbox<b> (6.1.38)

<h2>Walk-through: (Keep in mind that this is after initial setup of Windows 10/Windows server 2019 using Oracle Virtualbox)</h2>

<p align="center">
Set up IP Addressing for Windows Server 2019: <br/>


At the bottom right hand of the screen click the Network icon:  <br/>
![Screenshot 2022-10-02 013806](https://user-images.githubusercontent.com/114842751/193438218-675c118f-801c-4f30-92ca-3f7b42f97691.png)
<br />
<br />
Click on "Unidentified network: <br/>
![Screenshot 2022-10-02 014450](https://user-images.githubusercontent.com/114842751/193438261-ec6f2b65-acec-4911-997e-7d35767e2b1e.png)
<br />
<br />
Select "Change adapter options":  <br/>
![Screenshot 2022-10-02 014652](https://user-images.githubusercontent.com/114842751/193438302-f990ad1c-1158-4cf3-9182-bb74f7b42601.png)
<br />
<br />
From here you will have to determine between which of the 2 networks are your home (The one in the screenshot below is the VM IP so by default the other will be your home):  <br/>
![Screenshot 2022-10-02 015051](https://user-images.githubusercontent.com/114842751/193438404-d7d323c8-d603-41ce-a8ef-f476e22cae9b.png)
*Tip: Recommend naming different names for the networks so you can differeniate for the steps ahead.*
<br />
<br />
We need to give the Internal IP (VM) an IP address so Right Click on the Internal Ip and Click Properties:  <br/>
![Screenshot 2022-10-02 015919](https://user-images.githubusercontent.com/114842751/193438621-6a3b5528-6767-4615-a27f-998b9f71e21c.png)
<br />
<br />
When the window opens click on "(TCP/IPV4)" then click "Properties" this will pull up IPv4 Properties window:  <br/>
![Screenshot 2022-10-02 020221](https://user-images.githubusercontent.com/114842751/193438719-8d3be8d1-db29-4934-ac95-6c6201717730.png)
<br />
<br />
Click on "Use the following IP address" then type the following as shown in the screenshot: <br/>
![Screenshot 2022-10-02 020611](https://user-images.githubusercontent.com/114842751/193438818-d9349007-26bb-4e4f-a412-24542f909366.png)
<br />
<br />
Click OK and Close out of the Windows till you are back at the Server Manager Dashboard. <br/>
<br />
<br />

<p align="center">
Installing Active Directory Domain Services (AD DS)/ Creating Domain Admin User: <br/>
<br />
<br />

From Dashobroad, click on "Add roles and features" <br/>
![Screenshot 2022-10-02 021249](https://user-images.githubusercontent.com/114842751/193439003-cc8e3fa0-97ba-4cb6-8b74-8345608d9c40.png)
<br />
<br />

Click "Next" till you reach "Server roles" and add "Active Directory Domain Services": <br/>
![Screenshot 2022-10-02 021827](https://user-images.githubusercontent.com/114842751/193439142-19c1090d-653c-4c20-b679-7b2ddfc3da70.png)
<br />
<br />

Click "Add Features" when the window pops up, from there, click next till you reach the installation window and click "Install" (Installation may take longer depending on how you set up your Windows 2019 Server": <br/>
<br />
<br />

After installation click close and you will notice in the top right a flag symbol with a yellow caution sign: <br/>
![Screenshot 2022-10-02 022439](https://user-images.githubusercontent.com/114842751/193439335-5759b719-5546-4ca3-bdda-1d7a6c207547.png)
<br />
<br />

Click on the flag symbol and then where the caution message is click "Promote this server to a domain controller": <br/>
![Screenshot 2022-10-02 022641](https://user-images.githubusercontent.com/114842751/193439394-303cb6ea-7636-4779-856c-e03213aeb0e5.png)
<br />
<br />

Click on Add a new forest and then you can name the Root domain whatever you'd like: <br/>
![Screenshot 2022-10-02 022901](https://user-images.githubusercontent.com/114842751/193439502-000a33d6-c364-41d5-a968-05e5d803dad7.png)
<br/>
<br/>

Click Next and then set up a password for the Directory Services Restore Mode (DSRM) then click Next: <br/>
![Screenshot 2022-10-02 023353](https://user-images.githubusercontent.com/114842751/193439597-c48b9087-ad51-4702-834b-2f37a2c47e77.png)
<br/>
<br/>

Click Next till you reach the Installation page then click "Install" (This process may take awhile): <br/>
<br/>
<br/>

<p align="center">
Creating Dedicated Domain Admin Account: <br/>
<br />
<br />

From the Windows Screen click the Windows Button and click the Windows Administrative Tools tab, then click Active Directory Users and Computers: <br/>
![Screenshot 2022-10-02 074439](https://user-images.githubusercontent.com/114842751/193450100-381acaf2-6632-44d6-849e-ccddd2610033.png)
<br/>
<br/>

Then, right click on "mydomains.com" (In this case whatever you named your domain), Click "New", scroll to "Orginizational Unit" and click on that tab: <br/>
![Screenshot 2022-10-02 223244](https://user-images.githubusercontent.com/114842751/193486937-e4d043e2-d356-48d8-be8d-c212ba395997.png)
<br/>
<br/>

Once you have created the new object you will now name it (You can name it anything you want) then click "OK": <br/>
![Screenshot 2022-10-02 223559](https://user-images.githubusercontent.com/114842751/193487158-d2f3e983-ec6b-4884-9382-954018b9f033.png)
*Unclicking "protect container from accidental deletion" is optional*
<br/>
<br/>

Now right click the new object you just created, click "New", then click "User." <br/>
![Screenshot 2022-10-02 224803](https://user-images.githubusercontent.com/114842751/193487931-df17301a-99bb-4c51-81be-f3c9d272f748.png)
<br/>
<br/>

Next you will fill in the following with whatever you wish, this will signify the Admin login info. After filling in the info click "Next" <br/>
![Screenshot 2022-10-02 225244](https://user-images.githubusercontent.com/114842751/193488252-fd03d088-7506-4ff4-81a4-d1ceebac80f9.png)
<br/>
<br/>

Now that we are on the "create password page", create any password you like and since this is a conrolled lab, you can uncheck the "User must change password at next login" and then check "Password never expires" to keep it simple <br/>
![Screenshot 2022-10-02 225921](https://user-images.githubusercontent.com/114842751/193488738-168f757e-9245-4785-a8d9-9cef11420c21.png)
<br/>
<br/>

Click "Next" then click "Finish." <br/>
<br/>
<br/>

Now we need to make it an Domain Admin, so now right click on the newly created user and click "properties" then click "Member Of": <br/>
![Screenshot 2022-10-02 230422](https://user-images.githubusercontent.com/114842751/193489156-255e8398-cc4f-447c-b825-68107a829e80.png)
<br/>
<br/>

From there you will then click "Add" and then in the text box type, "domain admins" then click "Check Names", this will give you Domain Admins then press OK: <br/>
![Screenshot 2022-10-02 230750](https://user-images.githubusercontent.com/114842751/193489438-2ecd3896-7125-4bed-9ea2-95002c77d796.png)
<br/>
<br/>

Then highlight Domain Admins and then click "Apply" then "OK". Congrats! You created a Domain Admin account! <br/>
<br/>
<br/>

Now we need to sign out of the current account and login to our new admin account. <br/>
![Screenshot 2022-10-02 231206](https://user-images.githubusercontent.com/114842751/193489751-adf503d9-0007-420b-b6ea-999c383bd617.png)
<br/>
<br/>

<p align="center">
Creating RAS/NAT for private network for Windows 10: <br/>
<br />
<br />

For this next part you should be logged into your Domain Admin User account that we created together. <br/>
<br/>
<br/>

You will start by clicking on "Add roles and features" while in the Manager Dashboard: <br/>
![Screenshot 2022-10-02 231929](https://user-images.githubusercontent.com/114842751/193490363-a066fb3b-e839-451f-9bf1-93e97fa22413.png)
<br/>
<br/>

Once in, you will click "Next" till you reach "Server Roles" and you will select "Remote Access": <br/>
![Screenshot 2022-10-02 232124](https://user-images.githubusercontent.com/114842751/193490542-c834cfff-0e52-4420-9478-cd799f6222ef.png)
<br/>
<br/>

Click "Next" till you reach "Remote Access Role Services" and then click on "Routing": <br/>
![Screenshot 2022-10-02 232316](https://user-images.githubusercontent.com/114842751/193490714-b7a91b23-a637-49d6-9484-68bca0c40af1.png)
*DirectAccess and VPN (RAS) are automatically selected after clicking Routing, just leave it be*
<br/>
<br/>

Click "Next till you reach the Installation page and then click "Install" (This may take a bit to complete): <br/>
<br/>
<br/>

Once installation is complete, click "close and you will be back on the Dashboard, from there in the upper right hand corner click "Tools": <br/>
![Screenshot 2022-10-02 232804](https://user-images.githubusercontent.com/114842751/193491146-67151778-1099-4ce2-9085-090213e934a8.png)
<br/>
<br/>

Once open, scroll down to "Routing and Remote Access" and then click on it. Now a new window should pop up and You will see "DC(local)", right click on it and click "Configure and Enable Routing and Remote Access": <br/>
![Screenshot 2022-10-02 233128](https://user-images.githubusercontent.com/114842751/193491451-8e871096-e230-47e2-9f88-1e88bf430ee2.png)
<br/>
<br/>

A Setup Wizard window will pop up and will click "Next", then a configuration page will show and you will click "(NAT) Network Address Translation": <br/>
![Screenshot 2022-10-02 233348](https://user-images.githubusercontent.com/114842751/193491677-53d9c65e-4caa-4831-9977-c4cb863d9bac.png)
<br/>
<br/>

Click "Next", the next window should show the following information in the screenshot below, (If it does not, repeat steps from Tools on Dashboard and repeat till it does work. It will work eventually.): <br/>
![Screenshot 2022-10-02 233812](https://user-images.githubusercontent.com/114842751/193492117-45d8c651-1f30-46db-9360-8eab0416a136.png)
<br/>
<br/>

In the window click whichever you named that is connected to the internet (For me I named it internet), then click "Next" then "Finish:" <br/>
![Screenshot 2022-10-02 234034](https://user-images.githubusercontent.com/114842751/193492313-a113a04f-ab53-4e02-a93d-de951ca41edf.png)
<br/>
<br/>

Congrats! You just configured a NAT/RAS to your domain! <br/>
<br/>
<br/>

<p align="center">
Installing and Configuring DHCP: <br/>
<br />
<br />

While still logged into you Domain Admin User account, from dashboard you will click "Add roles and features": <br/>
<br/>
<br/>

Click "Next" till you reach "Server Roles", then select "DHCP Server", click "Add Features", click "Next" till you reach installation page then click "Install": <br/>
![Screenshot 2022-10-02 235232](https://user-images.githubusercontent.com/114842751/193493398-de3f0fd5-612b-425d-b120-e606ec804c9c.png)
*If steps followed correctly you should see this screenshot*
<br/>
<br/>

Close out of the window and you will be back in Dashboard and from there click on "Tools" in the right hand corner and then scroll till you see "DHCP" then click on that: <br/>
![Screenshot 2022-10-02 235714](https://user-images.githubusercontent.com/114842751/193493873-1e1233f9-6126-421b-839e-5d3137cbb24d.png)
<br/>
<br/>

The DHCP window will pop up, from there, click on the named domain, the drop box will show IPv4 and IPv6, right click on IPv4 and click "New Scope": <br/>
![Screenshot 2022-10-03 000202](https://user-images.githubusercontent.com/114842751/193494304-2d1a6b46-0836-404b-91e1-2c84827e57f7.png)
<br/>
<br/>

The Wizard Setup window will pop up and you will click Next, then you will name your Scope (I named it off the IP Range, you can name it whatever you wish):
![Screenshot 2022-10-03 000503](https://user-images.githubusercontent.com/114842751/193494547-c88732c0-fff0-4dd3-9b71-281625585a3d.png)
<br/>
<br/>

Next you will fill in the IP Range with the following: <br/>
![Screenshot 2022-10-03 000728](https://user-images.githubusercontent.com/114842751/193494736-5ad97f18-025d-4712-a1a8-69960efe0dc5.png)
<br/>
<br/>

Click "Next" till you reach "Router(Default Gateway)", then put in the following IP Address then click "Add": <br/>
![Screenshot 2022-10-03 001231](https://user-images.githubusercontent.com/114842751/193495154-edf37834-5d7e-4756-91fc-557341fd95ce.png)
<br/>
<br/>

Click "Next" till you reach the final page then click "Finish", then right click on the named domain, click "Authorize" then click "Refresh" and then your IP Addresses will light up green: <br/>
![Screenshot 2022-10-03 001737](https://user-images.githubusercontent.com/114842751/193495615-059d18df-4d57-424c-8b2b-d36513579aa8.png)
<br/>
<br/>

Congrats on setting up the DHCP, now close the window. <br/>
<br/>
<br/>

Now that we are back on the Dashboard, click "Configure this local server": <br/>
![Screenshot 2022-10-03 002045](https://user-images.githubusercontent.com/114842751/193495833-670407c0-7326-4bf3-8982-4a2ae6eec61f.png)
<br/>
<br/>

Next go to "IE Enhanced Security Configuration" and click on "ON" and turn it off for both admin and users: <br/>
![Screenshot 2022-10-03 002255](https://user-images.githubusercontent.com/114842751/193496053-6f5fd289-3f46-4fd5-accb-b90ff566f7fa.png)
*This will prevent spam notifications if it is on, since this is a home lab its not required*
<br/>
<br/>

Open Internet explorer and copy and paste the following link: <br/>
https://github.com/joshmadakor1/AD_PS/archive/master.zip
<br/>
<br/>

A pop up will open at the bottom, click "Save As" and save it to Desktop so its easier to find: <br/>
<br/>
<br/>

Minimize all the windows and extract the data from the folder: <br/>
![Screenshot 2022-10-03 003246](https://user-images.githubusercontent.com/114842751/193496864-53d6387a-e135-44e9-8e73-14b090d4b31c.png)
<br/>
<br/>

In the folder open up the "names.txt", at the top add your name and then save the txt file: <br/>
![Screenshot 2022-10-03 003450](https://user-images.githubusercontent.com/114842751/193497080-959b8d38-6d77-4536-bf58-39655d336c36.png)
<br/>
<br/>

Now click the windows button and open the Windows Powershell folder, righ click "Windows Powershell ISE", click "More", then "Run as Adminstrator": <br/>
![Screenshot 2022-10-03 003634](https://user-images.githubusercontent.com/114842751/193497324-07755b27-d96b-444a-8c04-d6a438d4ced8.png)
<br/>
<br/>

Now in Powershell, click file, scroll to desktop where the file is, click file, then click "1_CREATE_USERS": <br/>
![Screenshot 2022-10-03 004020](https://user-images.githubusercontent.com/114842751/193497599-d5924753-e6e5-4689-b5b0-0f1ff67674f5.png)
<br/>
<br/>

In the Command prompt you will type the following and press enter, a pop screen will appear and you press "Yes to All": <br/>
![Screenshot 2022-10-03 004333](https://user-images.githubusercontent.com/114842751/193497850-3b726968-5135-4ed0-a884-244d143d1ec1.png)
<br/>
<br/>

Next your going to change directory using the following command (Note: the name of the user account is based off the name you created): <br/>
![Screenshot 2022-10-03 031038](https://user-images.githubusercontent.com/114842751/193511544-a7e30214-0591-466a-bb2b-c26dfa197c39.png)
<br/>
<br/>

At the top of Powershell you will see a green play button called "run", click that. A pop window will appear, click "run once": <br/>
*This will create your user account you input in the names.txt file along with the other 1000 names and create user accounts through powershell* <br/>
![Screenshot 2022-10-03 031431](https://user-images.githubusercontent.com/114842751/193512011-edcd12bd-a148-45dc-94b6-0fd6f9b1210e.png)
<br/>
<br/>

<p align="center">
Windows 10 VM quick showcase: <br/>
<br />
<br />

When setting up your Windows 10 virtual machine, you will need to change the network Adapter 1 from NAT to Internal Network: <br/>
![Screenshot 2022-10-03 032727](https://user-images.githubusercontent.com/114842751/193513701-245ce110-2167-4c52-8ad9-d34bf215e48c.png)
<br/>
<br/>

When you get to installing it, make sure to choose "I dont have a product key" , and then choose "Windows 10 Pro": <br/>
![Screenshot 2022-10-03 033010](https://user-images.githubusercontent.com/114842751/193514392-a89c14d8-e18e-44ec-951f-eb67c691c96a.png)
<br/>
<br/>

Installation may take awhile. <br/>
<br/>
<br/>

Once installation is done for the WIndows 10 VM you'll want to check to see if it is connected to the internet. Open CMD and type in the following provided then press ENTER: <br/>
![Screenshot 2022-10-03 034534](https://user-images.githubusercontent.com/114842751/193516207-29abaa07-a891-4a2a-9614-a84f0e74db8d.png)
<br/>
<br/>

Next we want to hook up our CLIENT(Windows 10 VM) to the Domain we created so right click on the windows button in the bottom left corner, click on systems, scroll to "Rename this PC advanced)", click "Change", and type the following: <br/>
![Screenshot 2022-10-03 035315](https://user-images.githubusercontent.com/114842751/193517267-41db3125-e6c0-49be-bba3-57b8359cbd8b.png)
<br/>
<br/>

Click "OK" then you will need to put in the Domain Admin User info from before and then click "OK" and it will register and the you will be prompted to Restart, click "OK": <br/>
![Screenshot 2022-10-03 035706](https://user-images.githubusercontent.com/114842751/193517793-40600b15-27a1-4306-be37-77ca14032425.png)
<br/>
<br/>

Congratulations! You have basically created a mini corporation full of users. You would see this when joining a new company and the IT Admins would set up your account along with any new user in this type of fashion or something similar. <br/>
<br/>
<br/>
Thank you very much for checking this out!












</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
