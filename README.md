<h1>RODC (Read Only Domain Controller) Setup</h1>
<p>An RODC (Read-Only Domain Controller) maintains a read-only replica of the Active Directory database and prohibits any alterations to AD data. It is commonly deployed in branch offices, primarily due to insufficient physical security measures. If an unauthorized individual gains access to the RODC, they will be unable to modify the global data. Furthermore, if an intruder somehow succeeds in altering the data on the RODC, it won't be synchronized to writable DCs due to unidirectional replication (from writable to read-only DC).</p>
<h3>*Installation</h3>
<p>1. First we need to install Active Directory Domain Services(ADDS) on the Member server(MS1); from the server manager dashboard, click on Manage and on Add roles and Features</p>
<p align="center"><img src="https://i.imgur.com/BFw3fUz.png" height="50%" width="50%"/>

<p>2. On the before you begin screen, just click <b>NEXT</b></p>
<p align="center"><img src="https://i.imgur.com/gaMZiFi.png" height="50%" width="50%"/>

<p>3. On the Installation Type screen, make sure the Role-based or feature-based installation is selected, then click <b>NEXT</b>.</p>
<p align="center"><img src="https://i.imgur.com/ZvY3YRt.png" height="50%" width="50%"/>

<p>4. On the Select destination server screen, make sure the select a server from the server pool is selected and select the server you are trying to install Adds on from the server pool, then click <b>NEXT</b>.</p>
<p align="center"><img src="https://i.imgur.com/AAPGcSH.png" height="50%" width="50%"/>

<p>5. On the select server roles screen, select the second option(Active Directory Domain Services) and click on add features from the pop-up screen, then click <b>NEXT</b>.</p>
<p align="center"><img src="https://i.imgur.com/FJXu3HC.png" height="50%" width="50%"/>

<p>6. On the select features screen, just click <b>NEXT</b>.</p>
<p align="center"><img src="https://i.imgur.com/6Ri1r9H.png" height="50%" width="50%"/>

<p>7. On confirm installation selections, just click on INSTALL and wait for the installation to complete. </p>
<p align="center"><img src="https://i.imgur.com/qgNK3C5.png" height="50%" width="50%"/>

<br>

<h3>*Configuration</h3>
<p>1. After the installation is complete, from the notification, click on promote the server to a domain controller</p>
<p align="center"><img src="https://i.imgur.com/h2Ndsag.png" height="50%" width="50%"/>

<p>2. On the Deployment configuration screen, select “Add a domain controller to an existing domain”, then click on change to supply the domain controller’s Administrator’s credentials, then click <b>NEXT</b>.</p>
<p align="center"><img src="https://i.imgur.com/k4NRK0f.png" height="50%" width="50%"/>

<p>3. 3.On the Domain Controller Options screen, select Read only domain controller(RODC), type in the password, then click <b>NEXT</b>.</p>
<p align="center"><img src="https://i.imgur.com/3F3nYtL.png" height="50%" width="50%"/>

<p>4. On the RODC options screen, click <b>NEXT</b>.</p>
<p align="center"><img src="https://i.imgur.com/LTLnjle.png" height="50%" width="50%"/>

<p>5. On the Additional options screen, select the ADDS from the dropdown and click <b>NEXT</b>.</p>
<p align="center"><img src="https://i.imgur.com/YPkSrDk.png" height="50%" width="50%"/>

<p>6. On the Paths screen, leave it at default and click <b>NEXT</b>.</p>
<p align="center"><img src="https://i.imgur.com/rb6OlEy.png" height="50%" width="50%"/>

<p7. On the Review Options, click <b>NEXT</b>.</p>
<p align="center"><img src="https://i.imgur.com/deYa8py.png" height="50%" width="50%"/>

<p>8. On the Prerequisites Check, click <b>INSTALL</b>.</p>
<p align="center"><img src="https://i.imgur.com/STdtzNz.png" height="50%" width="50%"/>

<br>

<h3>*Checking RODC Replication Status</h3>
<p>1. To check RODC Replication on MS1; from the server manager-dashboard, click on Tools and go to Active Directory Users and Computers</p>
<p align="center"><img src="https://i.imgur.com/7A0a6W7.png" height="50%" width="50%"/>

<p>2. On the Active Directory Users and Computers page, expand the domain and click on the domain controllers, there you can find MS1 with the DC type as <b>“Read only,DC”</b></p>
<p align="center"><img src="https://i.imgur.com/gEMyhEt.png" height="50%" width="50%"/>

<br>

<h3>*Testing RODC Functionality</h3>
<p> Created a User on MS1 called Test User</p>
<p align="center"><img src="https://i.imgur.com/Bwyrg75.png" height="50%" width="50%"/>

<p><b>1. On Windows 10</b> - I changed the Alternate DNS Server on windows 10 to that of MS1(192.168.10.11), while the preferred DNS points to the ADDS(192.168.10.10), then I restarted the computer</p>
<p align="center"><img src="https://i.imgur.com/GTr1sjD.png" height="50%" width="50%"/>

<p>2. On the login page, I signed in the computer while I made sure the ADDS server is turned off and the Member Server(RODC) is turned on.</p>
<p align="center"><img src="https://i.imgur.com/Q4g70i2.png" height="50%" width="50%"/>

<p>3. I was able to sign in, this shows the functionality of the MS1 taking over the Active directory as a read only to authenticate users when the ADDS server is not available</p>
<p align="center"><img src="https://i.imgur.com/MylDXAp.png" height="50%" width="50%"/>

<br>

<h3>*CONFIRMATION WHILE ADDS IS OFF</h3>
<p>1. I also went back on the MS1 and from tools, clicked on Active Directory Users and Computers and got the message <b>“You are being connected to the Read-only Domain Controller MS1.adesakin.com. You will not be able to perform any write operation”</b>.</p>
<p align="center"><img src="https://i.imgur.com/WT9lloh.png" height="50%" width="50%"/>

<p>2. On the Active Directory Users and Computers, most of the buttons are greyed- out and couldn’t perform any write operations like create users or even edit. </p>
<p align="center"><img src="https://i.imgur.com/QmBLygF.png" height="50%" width="50%"/>

<br>



