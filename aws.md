# Setting Up My First AWS VM and Workspace

* Today I spoke with an AWS technician about how best to mimic the infrastructure I'd created on Azure and he suggested `AWS Workspaces` and said `VS Code` could *easily* be implemented there.

## Today (November 6, 2021)

### Prefatory Matters

* Step 0: I began by creating an instance of the free tier Windows 10 (Server 2016)
* Step 1: Then I created an AWS Workspace
* Step 2: The first thing that happened once I clicked on `Connect to Workspace` was to be taken to a **Directory Service** Wizard.
* Step 3: I selected `Simple AD` as the *Directory Type*, then I selected Small for the *Directory Size*.

```txt
Organization name: Treemore
Directory DNS Name: codecrazyaws.com [//]: # It had to be a FQDN.
Directory NetBIOS Name: codecrazy [//]: # This was not required.
```

* Step 4: Then I had to create an Administrator password and *Directory Description* where I placed the following:

    ```txt
    Simple AD for Treemore codecrazyaws.com with NetBIOS name codecrazy
    ```

* Step 5: I was then prompted click Next and was taken to Step 3 of the wizard titled **Choose VPC and subnets**
  * Note: <mark>VPC</mark> stands for **V**irtual **P**rivate **C**loud
  * A VPC is a "logically isolated virtual private cloud that lets you launch AWS resources in a logically isolated virtual network that you define" ([AWS Doc about VPCs](https://aws.amazon.com/vpc/)).
  * "The first step is to create your VPC. Then you can add resources to it, such as Amazon Elastic Compute Cloud (EC2) and Amazon Relational Database Service (RDS) instances. Finally, you can define how your VPCs communicate with each other across accounts, Availability Zones (AZs), or Regions" ([AWS Doc about VPCs](https://aws.amazon.com/vpc/)).
  * This comment had a [helpful graphic](https://d1.awsstatic.com/Digital%20Marketing/House/Hero/products/ec2/VPC/Product-Page-Diagram_Amazon-VPC_HIW.9c472d7f2eb39ab8bdd22aa3ab80be00cdd00d8f.png)
  * The VPC field was already populated with vpc-03f628223f1f60c54 (172.31.0.0/16)
  * There were two fields below for subnets but the default option was merely "no preference" so I left it.
  * At the bottom of this page there was a field which I was unable to edit called "Initial AD site name for this directory and it had called the directory `Default-First-Site-Name`.
* Step 6: After clicking next, I was taken to the "Review and Create" page.
  * I see it chose these subnets for me:
    * subnet-0366debd1b2ea5185 (172.31.16.0/20, us-east-1d)
    * subnet-03a70c3c277ce32b8 (172.31.0.0/20, us-east-1b)
  * Pricing is free for one month, then $.05 per hour or ~$36 USD per month.
  * I took a deep breath, then clicked "Create Directory."
* Step 7: The creation process succeeded but interestingly it displayed two directories which appear to have been created simultaneously.
  * One directory is coded with the *Directory ID* <mark>d-906752a6ac</mark> and has access to the Internet.
    * This directory has a *Directory Name* of `corp.amazonworkspaces.com` and is associated with organizaiton "d-906752a6ac"
  * The other directory is coded with the *Directory ID* <mark>d-906752c77b</mark> and has access no to the Internet
    * This directory has a *Directory Name* of `codecrazyaws.com` and is associated with organization "d-906752c77b".
      * Here is a [link](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/gsg_create_directory.html) to a tutorial about creating a directory.
* Step 8: Create a Workspace
  * It appears the first and most important step of this new process is to <mark>RTFM</mark> ([here](https://docs.aws.amazon.com/workspaces/latest/adminguide/launch-workspace-simple-ad.html#create-workspace-simple-ad)).

### Creating a New Workspace

* Step 1: Open [Workspaces Console](https://console.aws.amazon.com/workspaces/) and choose `Workspace` in the navigation pane.
* Step 2: Click "Launch Workspaces"
* Abandoned process (temporarily) after discovering Cloud Directories were available.

#### AWS Cloud Directories

* Step 0: Read the [documentation](https://docs.aws.amazon.com/clouddirectory/latest/developerguide/what_is_cloud_directory.html) about Cloud Directories. [//]: # It seems all the documentation is available at [https://docs.aws.amazon.com/](https://docs.aws.amazon.com/)
* This seems like a really great tool but for this initial test case the complexity is unnecessary.
* Returning to original process.us

### Creating a Workspace

* `Workspaces` are literally subtitled by AWS as "Desktops in the Cloud" which makes me think they are very similar to the Azure Virtual Desktops I've been failing to properly deploy for the past three weeks.
* Let's see if `Workspaces` actually *work* as *spaces* for the students.
* Let's further see how easy (read: intuitive) it is for a *novice user* like me to create and deploy one with `Visual Studio Code` installed.

#### Workspaces Configuration

* Once I clicked on the [Workspaces Console](https://console.aws.amazon.com/workspaces/) link a new tab opened and I was presented with what appeared to be an *already created* `Workspace`.
  * There was a ▶ button which, once clicked, presented information about the already created `Workspace`:

    ```txt
    Workspace ID: ws-fs8t82ls6
    Username: mmorelli
    Name: Morelli, Carlo
    Email: mmorelli@live.com
    Clients Link: [click here](https://clients.amazonworkspaces.com/) [//]: # The exact URL is https://clients.amazonworkspaces.com/, not too hard to remember.
    Registration Code: SLiad+ARZVCC
    Failure Message: None
    Connection State: UNKNOWN
    User Last Active: Information Unavailable
    Last State Check: Nov 6, 2021, 2:46:28 PM (just moments ago)
    Workspace IP: 172.16.0.113
    Launch Bundle: Standard with Windows 10 (Server 2019 based) (PCoIP)
    Language: English (US)
    Computer Name: WSAMZN-CTMFK52F
    Encrypted Volumes: None
    Encryption Key: None
    AutoStop Time: 1 hour
    State: None
    Tags: There are currently no tags associated with this WorkSpace
    Compute: Standard
    Root Volume: 80 GB
    User Volume: 50 GB
    Running Mode: AutoStop
    Status: STOPPED
    ```

* Since the `Workspace` was in STOPPED status, I clicked "Actions" and selected "Start Workspaces" and the `Workspace` `ws-fs8t82ls6` immediately started up.
* Then I selected the pre-configured `Workspace` named `ws-fs8t82ls6` and clicked on "Launch Workspaces."
* I was taken to a new page where (exactly as the documentation stated) I was asked to select a directory.
* I chose the one AWS had configured for me and **not** the one I created (since the one I created had no Internet access). 
  * The directory I chose was `d-906752a6ac` under the domain corp.amazonworkspaces.com.
* I clicked on the blue button "Next Step"
* I was then prompted to create users and discovered <mark>only 5 users may be created at a time</mark>.
* I clicked "Create Users" and nothing happened but the `Create New Users and Add Them to Directory: corp.amazonworkspaces.com` prompt appeared again so I continued adding my students to the directory.
* The following users were created: (the actual user information is redacted for privacy reasons but is available to me.)

    <!-- No. |              Username                |          Name             |          Email
    --- | ------------------------------------ | ------------------------- | -----------------------------
    1   | corp.amazonworkspaces.com\azubair    | Afshaal Zubair            | afshaalzubair@outlook.com
    2   | corp.amazonworkspaces.com\darackal   | Daniel Arackal            | daniel.arackal.3@gmail.com
    3   | corp.amazonworkspaces.com\ggiambi    | Gianmarco Giambi          | gianmarcog4805@gmail.com
    4   | corp.amazonworkspaces.com\tdean      | Tyler Dean                | tylerdean805@gmail.com
    5   | corp.amazonworkspaces.com\aowens     | Austin Owens              | owensaustin19@gmail.com
    6   | corp.amazonworkspaces.com\cliu       | Chen Liu                  | ff0989116301@gmail.com
    7   | corp.amazonworkspaces.com\wmahabani  | Wassime Mahabani          | wassimf05@gmail.com
    8   | corp.amazonworkspaces.com\jcontreras | Josue Contreras           | josuec1744@gmail.com
    9   | corp.amazonworkspaces.com\rskinner   | Ryan Skinner              | rs0619tx@gmail.com
    10  | corp.amazonworkspaces.com\mtsao      | Michael Tsao              | mctsao1115@gmail.com
    11  | corp.amazonworkspaces.com\mike       | Michael Morelli           | teachermorelli@gmail.com
    12  | corp.amazonworkspaces.com\rflickner  | Ron Flickner              | rflickner@live.com
    13  | corp.amazonworkspaces.com\mmohammed  | Abdul-Muhaymin Mohammed   | amohammed8135@gmail.com -->

* 13 Users were created and automatically below a list appeared of Created `Workspaces`: One for each user. They were all there, *very helpfully* pre-selected and added to the list for deployment.
* Then I clicked on "Next Step." [//]: # So far the UI/UX has been buttery smooth, esp. comp. to Azure
* I had to choose which `Bundle` (VM image) to attach *to each user* so I selected the Free Tier Standard with Windows 10 (Server 2019 based) ([WSP-based](https://docs.aws.amazon.com/workspaces/latest/adminguide/amazon-workspaces-protocols.html)) which includes:
  * 2 vCPUs
  * 4 GiBs RAM
  * 80 GBs Root Volume Storage
  * 50 GBs User Volume Storage

* After clicking "Next Step" I was prompted to select a "Running Mode" and this was about *billing*.
  * The options were "AlwaysOn" (billed monthly) and "AutoStop" (default for free-tier set to 1 hour)
    * I chose the default selection of AutoStop which is billed **by the hour**. It saves the state of the user each time they log off and stops the billing until they log back in.
* I skipped Encryption because it looked like a nightmare.
* For tages I gave Key=Name and Value=Workspace
* I was then prompted with "Create Workspaces" and off to the left it indicated the location of the physical hardware was northern Virginia (the only place in the country where AWS has these free workspace instances available, according to the technician I spoke with).
* When I clicked "Create Workspaces" I was prompted with a notification that my free tier only permitted the creation of 10 workspaces (and I was provisioning 13 of them) so I went back and de-selected my fake account, Ron's account, and Ryan Skinner (since he's going to get his own special system, perhaps along with Wassime). 
* Then I went through the next few steps again and provisioned as stated above.
* Once again, I got the prompt, so I went back and removed Wassime, then finally I was able to create 9 (not 10, as indicated was the max) workspaces.
  * Ah, now I understand why: My own Global Administrator account mmorelli was one of the workspaces.
  * That makes sense.
* Every user's workspace was given a unique identifier so I put those next to their names in my Excel file.
* The deployment message indicated it could take 20 minutes to provision and deploy the workspaces so I decided to explore "Applications" along the left navigation pane.

### Applications

* I was immediately presented with "Select a Subscription Plan" ([learn more](https://aws.amazon.com/workspaces/applicationmanager/#pricing)) so I went with "WAM Lite" since it was <mark>entirely free</mark> and the "WAM Standard" additional features didn't seem worth $5/month extra.
  * This screen also indicated each application is *billed separately*.
* I was then presented with two options from where I may find applications: 1) "Your Own Applications" and 2) "Source: AWS Marketplace" so I selected option 2.
* I then clicked "Add an application from AWS Marketplace" hoping VS Code was among them.
* The following *relevant* applications (there were 141 apps) are *entirely free*:
  * VLC Media Player
  * PuTTy
  * Silverlight
  * Python 2.7.8
  * Atom Editor
  * R
  * Firebird (OSS SQL)
  * jEdit (Java IDE)
  * Git
  * ThinPrint Cloud Printer (not free but only 1.18/mo/user and allows printing to local printer)
  * CutePDF Writer
  * Mozilla Firefox
  * Python 3.x (Version 3.5.2)
  * Foxit Reader (PDF Reader/Filler)
  * 7Zip
  * SquirrelMail (POP/IMAP Client)
  * Handbrake
  * Eclipse IDE
  * Notepad++
  * Audacity
  * Inkscape (Vector Graphics Editor like Adobe Illustrator)
  * GitHub (not quite sure *what exactly* this is...though I imagine it is GitHub Desktop; also, it requires .NET framework to run which I am uncertain is pre-installed or costly to install)
  * VIM
  * Strawberry Perl (Perl IDE)
  * KompoZer (a WYSIWYG html editor)
  * <mark>NO VS CODE</mark>

* Given the available options, I chose Git as a starter; eventually I'll install most, if not all, of the applications listed above.
* I clicked on the application and was taken to a page which had an orange button labeled "Continue" so I clicked it, then the next page gave me an orange button labeled "Subscribe" so I clicked it and it changed from "Subscribe" to "Subscrib**ed**".
* There is an optional [local, plaform independent (including Andoid and iOS client](https://clients.amazonworkspaces.com/) which can be downloaded to access the user workspace or you can access it directly from the web.
  * I downloaded the 64-bit client for Windows.
    * Once downloaded, I opened the client and was prompted to enter a registration code.
    * I visited my email and found it in my Junk folder (I'll have to remember to tell the students this).
    * To simulate the actual experience of most of the students, I decided to wait on using the local client and clicked the registration link in my email which was accompanied by a `special registration code`; however, when I clicked the registration link I was not prompted to enter a registration code; instead, I was merely prompted to enter a new password. 
    * I was then redirected to the same page where I downloaded the client, only this time I noticed one of the options alongside the local clients was "Web Access" so I clicked on it.
      * Note: When you hover over Web Access it says "Launch"
      * This is the URL for Web Access to Workspaces: [https://clients.amazonworkspaces.com/webclient#/registration](https://clients.amazonworkspaces.com/webclient#/registration).
      * Aha, now, I was prompted to enter a registration code, so I went back to my email, copied it to the clipboard, and pasted it into the registration code box, then clicked on the blue button that read "Register".
        * Uh oh, an error was displayed:

        ```txt
        Error
        An error occurred while loading the Authentication page. Please make sure Web access has been enabled for the directory containing the workspaces.

        If the problem persists please contact your WorkSpaces administrator.
        ```

    * This seems fixable. It seems I need to enable Web Access in the directory. Now, how to do that? *Maybe* I should <mark>RTFM</mark> ([here](https://docs.aws.amazon.com/workspaces/latest/adminguide/launch-workspace-simple-ad.html#create-workspace-simple-ad)).
    * Of course, navigating back to the Directory I chose above revealed this was not enabled:

    ```txt
    Application access URL Info
    The public endpoint URL where users in this directory can gain access to your AWS applications and to your AWS Management Console.
    ```

    * So I clicked on "Create" and was prompted to enter an alias such that the address students navigate to for Web Access is https://alias.awsapps.com so I used `codecrazy` as the alias and clicked the orange button labeled "Create".
    * Once that was done, I was returned to the previous screen and I clicked on "Enable" to enable the newly created Application Access URL https://codecrazy.awsapps.com.
    * A pop-up was shown with this information:

    ```txt
    Enable single sign-on
    This will enable users in your directory to seamlessly access AWS applications from a computer joined to this domain.


    Would you like to enable single sign-on for this directory?

    Note: We recommend that you first update your end-user browser setting before you enable single sign-on. Learn more
    ```

    * Following that "Learn more" button I was directed to [this page](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_single_sign_on.html?icmpid=docs_dirservices_console) which indicated only AWS Directory Service provides SSO login. 
    * Recall earlier I had specifically *not* chosen this type of directory and had instead chosen the <mark>Simple AD</mark> directory service. Hmm.
    * Luckily, there was a [link](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_migrate_users.html) just to the left of this article in the navigation pane which was titled "Migrate users from AD to AWS Managed Microsoft AD" along with [this](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_management_console_access.html) link which was titled "Enable access to the AWS Management Console".
      * It turns out the Migration link was for on-prem migration...not what I needed.
      * **This was an easy fix**: I just returned to the Directory page, clicked on the directory I had used to provision the Workspaces, and clicked "Enable" below this text:

    ```txt
    Application access URL Info
    The public endpoint URL where users in this directory can gain access to your AWS applications and to your AWS Management Console.

    Access URL:
    codecrazy.awsapps.com
    Amazon WorkDocs single sign-on Info
    (Enable button)
    ```

    * I clicked the "Enable" button.
      * Note: Below this button were a number of disabled services, one of which was "AWS Single Sign-On (SSO) but upon clicking [this link](https://console.aws.amazon.com/singlesignon/home?region=us-east-1#/) I discovered it is only available in the US East (Ohio) region but my Workspaces are located in the northern Virginia region. As the link states, "AWS Organizations can only support one AWS SSO region at a time. To enable AWS SSO in this region, you must first delete your current AWS SSO configuration in that region."
      * Note 2: I also noted that WorkDocs *and* WorkSpaces were *already enabled* **before** I hit that Enable button
        * It turns out I already [have a link](https://d-906752a6ac.awsapps.com/workdocs) to WorkDocs, which is, according to [this site](https://aws.amazon.com/workdocs/?amazon-workdocs-whats-new.sort-by=item.additionalFields.postDateTime&amazon-workdocs-whats-new.sort-order=desc), "a fully managed, secure content creation, storage, and collaboration service. With Amazon WorkDocs, you can easily create, edit, and share content, and because it’s stored centrally on AWS, access it from anywhere on any device."
    * Let's return to me hitting that "Enable" button. When I clicked it, a green check box banner appeared which read "You have successfully enabled Amazon WorkDocs single sign-on."
    * I figured, "Let's try connecting to that Web Client again."
    * So I navigated to our new aliased URL, [codecrazy.awsapps.com](https://codecrazy.awsapps.com), and was prompted to enter my email address to login to *WorkDocs*...no, this isn't what I wanted.
    * I decided to go back to that site where I had downloaded the local client and clicked on [Launch Web Access](https://clients.amazonworkspaces.com/webclient#/registration).
    * Once again, it failed with the same error as before. It seems I **must** have AWS SSO abilities...darn, gonna have to troubleshoot that.
      * But before getting into that, I decided to try the local client I had downloaded.
        * Just as with the Web Access Portal, I was prompted to enter a registration code. Upon doing so, I was prompted to enter my username and password and then click sign in.
        * I was prompted with a Windows Defender Firewall warning and granted access.
    * I was immediately delivered to a Widows desktop. I noted that **Git**, the program I had selected to install, did not appear to be installed; however, I went ahead with my first order of business: Install Chrome. (The desktop came with IE and Firefox preinstalled.)
      * The version of Chrome that was installed was Version 95.0.4638.69 (Official Build) (64-bit)
      * The latest version of Chrome is Version 95.0.4638.69 (Official Build) (64-bit) so it really did install the latest version of Chrome!
      * Now for the big questions:
        * What about Git, WSL, Ubuntu, and of course, <mark>Visual Studio Code</mark>?
          * I also need to update PowerShell to 7.x, install Terminal, and several other applications. Let's see how this goes.
        * We must install those programs in a special order such that the $PATH inheritances occur without error. I don't *think* it matters whether I install Git before WSL; however, just to be on the safe side, I am going to install WSL *first*, then Git, then Ubuntu, and *then and only then*, VS Code. The remaining programs are order independent.

### Configuring and Customizing the Virtual Desktop/AWS WorkSpace
* Note: I am doing all this from the desktop connector client because we still have to troubleshoot that web connect issue above. Actually, before I do any of this I will create a support ticket about that--the last time I created a ticket Amazon called **INSTANTLY** and a tech was on the phone (same price: $100/month for phone support but *so much faster*).
  * I created a support ticket and was **instantaneously** called by Amazon...*amazing*.
  * I'm going to put this markdown file online so the engineer can look at what I did.
  
### How The Problem of Web Access Was Fixed!
* First, the technician had me go to workspaces
* Then, he had me click on directories
* Then, he had me select the directory that I had used to create the Workspaces.
* Then he had me click on Actions
* Then he had me cick on Update Details from the dropdown menu
* Then he had me click on Access Control options
* Then he had me CHECK THE BOX that was *unchecked* that had the label **Web Access**.
* Then he had me click on the blue button in the bottom right corner of the screen labeled "Update and Exit"

#### Error Again
* We tried to connect to the Web Client and *this time* I got passed the registration information prompt and was actually able to enter my username and password; however, the system just spun a circle for several seconds (perhaps 90 seconds) before timing out and failing with this error:

    ```txt
    Error
    An error occurred while connecting to your WorkSpace.

    If the problem persists please contact your WorkSpaces administrator.
    ```

* The technician thought at first there might have been an issue due to the fact that I was *still logged in* to my Workspace session from the *locally insalled access client*, which made sense to me too, so I signed out of it (I did not just exit the window, I signed out properly by clicking start, sign out, etc.).
* We then tried to reconnect and got the same error.
* This technian is very clever: He had me click the vertical elipses 
* ​

​

​

​

​

​

https://docs.aws.amazon.com/workspaces/latest/adminguide/web-access.html#configure_group_policy


Error Log for Web Access #1 [link](https://www.dropbox.com/s/zbn8w6vpijymnzx/AWSREMOTEHOSTFAILURELOGclients.amazonworkspaces.com.har?dl=0)

Error Log for Web Access #2 [link](https://www.dropbox.com/s/vuxc3pn61kde6qs/SECOND_ATTEMPT_AFTER_SERVER_CONFIG_AWSREMOTEHOSTFAILURELOGclients.amazonworkspaces.com.har?dl=0)