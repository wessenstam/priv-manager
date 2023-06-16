# Global Policies

## Overview

This module will cover:

1. Policy Creation Methodology
2. Denylisting (blocking application execution)
3. Executable Elevation Policies
4. Installer Elevation Policies

## Policy Creation Methodology

A general rule of effective policy creation (although there are exceptions) is that individual policies should be structured from the most granular down the broadest **catch all** policies. Similar approaches are typically used when creating firewall rules as a point of reference.
The diagram below illustrates this concept:

![](images/lab-pv-001.png)

!!!Note
    A key principle of effective policy design is to ensure that any given application cannot pass through the policy set without, at the very least, matching against the catch all policy.

In the following lab exercises we will now create a range of policies based on the principles explained above but also taking into consideration the fact that most organizations have multiple types or communities of users who require different types of endpoint experience.

## Denylisting (blocking application execution)

Creating a policy to prevent applications which are known to be malicious or inhibit user productivity is a very common use that can easily be fulfilled with Privilege Manager. When creating a denylisting policy, it will typically be the first policy in the set with the lowest priority level. This avoids any risk of any other policies inadvertently allowing an application to run which we intent to block.

!!!Note
    Although deploying denylisting policies is common, it is important to note that denylisting on its own is not an effective approach to creating a secure endpoint application environment. The reason for this is that a denylist represents a point in time snapshot of applications. There are constantly new, unknown applications that cannot be targeted. In further modules we will explore how a combination of denylisting, allowlisting and execptionlisting can be used to create a secure environment.

### Lab 15 - Creating a denylisting (blocked application) policy

Before starting the lab exercise, we will disable the **Monitor Applications Run with Administrator Rights Policy** we created earlier in Module 6 as the policy set we are creating will also capture valuable discovery events. To disable this policy

1. Navigate to **WINDOW COMPUTERS group > Application Policies**

2. Search the **Monitor Applications Run with Administrator Rights Policy** and click the toggle switch so it shows **Inactive**

    ![](images/pm-0001.png)

We are going to use the Wizard again to create the blocking policy to not allow the use of Internet Explorer and show a message that the application is not allowed.

01. Click **Create Policy**

02. Click **Controlling** and click **Next Step**

03. Click **Block** and click **Next Step**

04. Click **Notify and Block** and click **Next Step**

05. Click **Executables** and click **Next Step**

06. Click **Existing Filter**

07. In the new screen, use the Magnifier Glass and type *Internet* and click the **Add** text in the line where you see Internet Explorer

    ![](images/pm-0002.png)

08. Click **Update**

09. Click **Next Step**

10. Use the following parameters for the fields:

    - **Name:** Global – Blocked Applications
    - **Description:** This policy blocks defined applications for all users
    - **Priority:** 1

11. Click **Create Policy**

12. Activate the policy by clicking the **Inactive** toggle switch

To test the policy we are going to login to the **CLIENT** machine.

01. Switch to the CLIENT machine

02. Sign out the current user

03. At the login screen, click **Other user**

04. Use **standarduser** / *Password provide by trainer*

    !!!Note
        As the installation has been updated, it will take some time before the user is logged in. It may take approx 2-5 minutes. A good time to get a drink or stretch your legs.

05. Navigate to **C:\\Program Files\\Thycotic\\Agents\\Agent** and double click **Agent Utility**

06. In the UAC screen use the **thylab\\adm-training** user and corresponding password to run the application. The StandardUser is NOT an administrator on the VM

    ![](images/pm-0003.png)

07. In the Agent Utility click the **View Cache** button to view the policies. The newly created policy should be shown

    ![](images/pm-0004.png)

    !!!Note
        If the policy is not shown, click the **Update** button to get the policy on the system.

08. **Close** the *Cache Viewer*

09. Try to open Internet Explorer by using any know method.

10. The start of Internet Explorer should trigger the block policy and show an **Application Denied** message as shown below.

    ![](images/pm-0005.png)

11. Click **Close**

## Executable Elevation Policies

In this module we will explore and create policies to elevate applications. When a user logs in to a Windows machine, a component of the operating system (local security authority) generates a user access token, in most scenarios this access token is then passed to applications that the user runs. This means that if the user is logged in as an admin, applications run with admin rights. If the user is a standard user, applications run with standard user rights. Privilege Manager can target specific applications and elevate the privileges that the application runs with.

A common approach is to target executable applications and installers that require elevation in separate policies. We will now create both policies:

### Lab 16 - Creating an executable elevation policy

We are going to use the Wizard again to create the blocking policy to not allow the use of Internet Explorer and show a message that the application is not allowed.

01. Switch back to **SSPM**

02. Navigate to **WINDOW COMPUTERS group > Application Policies**, or click the **Back to Applications Policy** text in the top left corner of the middle pane

03. Click **Create Policy**

04. Click **Controlling** and click **Next Step**

05. Click **Elevate** and click **Next Step**

06. Click **Run Silently** and click **Next Step**

07. Click **Executables** and click **Next Step**

08. Click **Existing Filter**

09. In the new screen, use the Magnifier Glass and type *dfrgui* and click the **Add** text in the line where you see *Defragment GUI Utility (dfrgui.exe)*

    ![](images/pm-0006.png)

10. Click **Update**

11. Click **Next Step**

12. Use the following parameters for the fields:

    - **Name:** Global – Elevated Executable Applications
    - **Description:** This policy elevates corporately approved applications that require admin rights for all users
    - **Priority:** 10

13. Click **Create Policy**

#### Using Policy Events to add applications to policies

Now that we have the policy created, **don't** set the policy to Activate. We want to add another application, but we are going to do that via the Policy Events, the discovered applications.

01. In the Privilege Manager UI open **Policy Events**

02. Click on **New Loaded Resource** a new navigation bar will open to the right. Click **View File** and click **Discover Now**

03. Click the **Back to Policy Events**, refresh the browser screen and click **Agent Utility.exe** and  to see the details on the right hand slide

04. Click **Create Filter**

05. Set the checkbox for **Original File Name**

    ![](images/pm-0007.png)

06. Click **Create and Add to Policy**

07. In the next screen, select **Global - Elevated Executable Applications** from the dropdown box

    ![](images/pm-0008.png)

08. Click **Update Policy**

09. This will revert back to the policy. Under **Applications Targeted** a line shows the *Agent Utility.exe* mentioned

    ![](images/pm-0009.png)

10. Under the **Conditions** section, click **Exclusions** and add the **Administrators** group.

11. Click **Update**

12. That way we don't run the policy against the Administrators in the system.

13. Under the **Actions** section click **Add Child Actions** and add **Add Administrative Rights**

14. Click **Update**

    ![](images/pm-0010.png)

    !!!Note
        This ensures that child processes of this application will have the same actions applied as the parent. In some cases, it can be dangerous to elevate child processes from some applications so this setting should be used with caution. The policy set we are creating will also pass child processes back through the entire policy set to ensure every child process is checked against denylists and other policies

15. Click **Show Advanced** text and enable **Continue Enforcing Polices** by clicking the toggle switch

    ![](images/pm-0011.png)

16. Click **Save Changes**

17. Activate the policy by clicking the **Inactive** toggle switch

#### Testing the created policy

1. Switch to **CLIENT01**

2. Click the **Update** button in the Agent Utility

    !!!Note
        If you closed the Agent Utility, open it again by:

        - Navigate to **C:\\Program Files\\Thycotic\\Agents\\Agent** and double click **Agent Utility**
        - In the UAC screen use the **thylab\\adm-training** user and corresponding password to run the application. The StandardUser is NOT an administrator on the VM

        ![](images/pm-0003.png)

3. The just created policy should be shown in green.

4. Close the Agent Utility and reopen it. There should not be any UAC prompt as the application is allowed and "automagically" elevated

## Installer Elevation Policies

Many installers are provided by software vendors as an executable file, in this case the application can be targeted like any other .exe file with the policy created in the previous exercise. If installers are provided in a .msi format, then the policy configuration needs to be slightly different.

When a .msi (Microsoft Installer) is executed within Windows, a separate executable is called (msiexec.exe). This is a Windows application used to run the installation. The Privilege Manager policy will need to elevate this executable application for the specific .msi files we target.

### Lab 17 - Creating an installer elevation policy

01. Switch back to **SSPM**

02. Navigate to **WINDOW COMPUTERS group > Application Policies**

03. Click **Create Policy**

04. Click **Skip the wizard, take me to a blank policy** as we want to control all steps and options ourselves

05. Use the following parameters for the fields shown:

    - **Name:** Global – Elevated Installers (msi)
    - **Description:** This policy elevates defined installers for all users
    - **Priority:** 15

06. Click **Create Policy** and let's populate the needed fields so we create our policy

07. Under **Conditions** section, click **Add Inclusions** and add the *Microsoft Installer File Filter (msiexec.exe)* like before

08. Click **Update**

09. Under **Actions** section, click **Add Actions** and add the **Add Administrative Rights**

10. Click **Update**

11. Under **Actions** section, click **Add Child Actions** and add the **Add Administrative Rights**

12. Click **Update**

13. Click **Show Advanced** text and make sure **Continue Enforcing Polices** and **Continue Enforcing Policies for Child Processes** are toggle on

14. The policy should look like the below (with respect to Conditions, Actions and Policy Enforcement)

    ![](images/pm-0012.png)

15. Click **Save Changes**

    !!!Note
        If we left the policy in its current state and applied it, all .msi files would be elevated as we are currently elevating msiexec.exe whenever it runs. To change this behavior, we will now target the specific .msi files we want to elevate

16. Open a new browser tab and navigate to <https://7-zip.org/download.html>

17. Select and download the 64bit msi installer

    ![](images/lab-pv-014.png)

18. In the Privilege Manager UI, select **Admin > File Upload**

19. Click **Upload File**

20. In the new screen click **Choose File** and navigate to the just download .msi file

21. Click **Upload File**

22. After the upload and the inventory has been done, click **Go to File Details**

    ![](images/pm-0013.png)

23. You see now the details as discovered after the File Upload phase.

24. Click **Create Filter**

25. Select the **File Name** and click **Create and Add to Policy**

26. Select the **Global - Elevated Installers (msi)** policy

27. Click **Update Policy**, the policy will open

    !!!Note
        Under the **Conditions** section note that the filter has been created as a **Secondary Filter**. This means that filter is treated as a secondary file filter to the msiexec.exe we defined in the **Inclusions**. This means that the msiexec application will only be elevated if it is called to install the 7-zip installer.

28. Set the policy to **Active** by clicking the **Inactive** toggle switch

#### Testing the created policy

1. Switch to **CLIENT01**

2. Click the **Update** button in the Agent Utility

    !!!Note
        If you closed the Agent Utility, open it again by:

        - Navigate to **C:\\Program Files\\Thycotic\\Agents\\Agent** and double click **Agent Utility**
        - As the *Global – Elevated Executable Applications* policy is active, there will not be an UAC message

3. The newly created policy should be shown in green

    ![](images/pm-0014.png)

4. Open Chrome browser and download the same 7-Zip installer

5. Start the installation process of the 7-Zip msi file

6. The installation should be elevated and succeed without any UAC prompt throughout the installation process.

7. To test another msi, download the putty msi installer from <https://the.earth.li/~sgtatham/putty/latest/w64/putty-64bit-0.76-installer.msi> (or use Google to find the URL)

8. Start the Putty installer, follow the installer and you will see the UAC prompt after a few steps. **NOT AT THE BEGINNING OF THE INSTALLATION!!!!**. As the StandardUser is not an Administrator, the UAC asks for credentials.

9. Cancel the installation by clicking **No** in the UAC

    ![](images/lab-pv-017.png)
