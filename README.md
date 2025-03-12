<h1>Group Policy and Managing Accounts</h1>

<h2>Overview:</h2>

- <b>Account Lockout Policy – Configure Group Policy to lock out accounts after failed attempts.</b> 
- <b>Enable and Disable Accounts – Test account login behavior after enabling/disabling accounts.</b>
- <b>Resetting Passwords</b>
- <b>Log Monitoring – Observe authentication and security logs.</b>

<h2>Configure Group Policy to lockout account</h2>

On DC-1, open Group Policy Management <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.1%20group%20policy%20management.PNG)
<br />

Under mydomain.com, right click the Default Domain Policy -> Edit <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.2%20edit%20default%20domain%20policy.png)
<br />

Go to Computer Configuration -> Policies -> Window Settings -> Security Settings -> Account Policies -> Account Lockout Policy <br/>
See the policies in place<br/>
Click on Account lockout duration to view properties<br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.3%20expand%20tree.PNG)
<br />

Make sure Define this policy setting is checked <br/>
Set account locked out for 30 minutes <br/>
Click Apply, then OK  <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.4%20account%20lockout%20duration.PNG)
<br />

Some suggested values are generated  <br/>
Click OK  <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.5%20suggest%20value%20changes%20ok.PNG)
<br />

View our current settings now in place  <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.6%20policy%20settings.PNG)
<br />

Log in the CLIENT-1 as jane_admin update policy for users <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.7%20login%20client1%20as%20janeadmin.PNG)
<br />

Update the group policy <br/>
Open the cmd  <br/>
Enter "gpupdate /force" <br/>
Updates successfully<br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.8%20gpupdate%20on%20cmd.PNG)
<br />

Log in to CLIENT-1 as our random user to test password policy<br/>
When we enter wrong password 6 times it locks us out<br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.8%20failed%20login%20locked.PNG)
<br />

<h2>Unlock the account</h2>

On DC-1, right click on our locked out user -> Properties  <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/13.4%20pick%20random%20user.PNG)
<br />

Check Unlock Account <br/>
Click Apply and Enter <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.9%20unlock%20account.PNG)
<br />

Log in to CLIENT-1 and enter the credentials as our user<br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.10%20login%20client1%20as%20cikoredo.PNG)
<br />

Open Powershell or cmd <br/>
Enter whoami command to show we are logged in CLIENT-1<br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.11%20powershell%20whoami.PNG)
<br />

<h2>Reset Password</h2>

In DC-1, right click on our user -> Reset Password <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.12%20reset%20password.png)
<br />

Enter a new password and ensure the Unlock users account is checked  <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/14.13%20create%20new%20password.PNG)
<br />

<h2>Enabling and Disabling Accounts</h2>

Right click user -> Disable Account <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/15.1%20disable%20account.png)
<br />

Account has been disabled <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/15.2%20account%20disabled.PNG)
<br />

Attempt to login on CLIENT-1 <br/>
The account is currently disabled <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/15.3%20attempted%20login%20account%20disabled.PNG)
<br />

<h2>Observe logs in Event Viewer</h2>

Open Event Viewer <br/>
We can see the failed attempts as Audit Failure and Event ID 4625  <br/>
We can also see the succesful login as Audit Success and Event ID 4624 <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/16.1%20event%20viewer%204625%20audit%20failure%20audit%20sucess.PNG)
<br />
