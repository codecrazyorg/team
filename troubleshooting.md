# MORELLI AZURE DANTE-ESQUE CIRCLES OF HELL NIGHTMARE TROUBLESHOOTING DOC

## Account Details

### Current Live and Active Account Linked to Most Current and Primary Support Request ID 2111050040007156
* Note: Support Request ID 2111050040007156 is linked to, built upon, and was initiated by a request\
from engineer Amit who was attempting to resolve Support Request ID 2111050040000938

#### Organization
* Treemore LLC
* Treemore Azure Tenant ID: f3061bf4-67d3-4727-9b5c-e8d05a9a5e4e
* Treemore Azure Directory ID: f3061bf4-67d3-4727-9b5c-e8d05a9a5e4e
* Treemore Azure Subscription ID: f31ae3bb-1685-4331-975d-fbb97598b68b
* Linked Microsoft Office 365 ID: 10032001A1E5A1ED
* 
#### Global Account Administrator
* Name: Carlo Morelli
* Azure Username: mmorelli@treemore.com
* Personal Cell Phone (iPhone): +1 9039486000
* Email: carlo.m.morelli@outlook.com
* Alternate emails: mmorelli@live.com; mmorelli@treemore.com; teachermorelli@gmail.com; carlo.morelli@lcisd.org

### Previous Accounts Dealing with the Same Issue
* Note: The below accounts are still being billed; still active; **I'm a high school teacher...**\
*There must come an end to all this soon*, I can't afford to pay $3K+/mo. for 3 accounts.\
The *only account which should be active*; the *only account* which should have *any* billing,\
is the one indicated above: **Treemore LLC/mmorelli@treemore.com**.\
**Any other existing accounts** and their associated subscriptions, resources, hosts, tenants,\
organizations—literally *anything* linked to the accounts below should be **terminated and deleted** *immediately*.

#### Most Recent Now-Moribund and Essentially Dead and Functionless Account
* carlommorellioutlook.onmicrosoft.com <-- default domain for the new Azure tenant
* Tenant ID: `2c68e9d5-7255-4a9d-9a6b-95cf341945f7`
* carlo.m.morelli@outlook.com (super user)
* Subscription directory: `Code Crazy (2c68e9d5-7255-4a9d-9a6b-95cf341945f7)`
* There is no `Management Group`.
* A group called AAD DC Administrators was created automatically...not sure what it means or who is in it or who controls or who owns it.

## History of All Accounts Troubleshooting Efforts and Cases in Chronological Order

### TROUBLESHOOTING USER ACCESS ERROR TO WVD/AVD

##### Actions Taken to Resolve AVD/WVD User/Group Session Error "Your do not have access to this resource"

###### First thing I did at 7:45 AM CDT on 10-30-2021
* Created IAM Role Assignment to AVD/WVD Virtual Machine Code-Crazy-0 granting role Virtual Machine User Login to Group "Programmers". 
* Programmers has type "Security Group" and Object ID of 
ed61d18b-2055-461d-b619-f9110ad49971 and is type "Group".
* The scope of this Role Assignment is: /subscriptions/b520aa79-4f34-44f6-af71-8b5711f5d0e6/resourceGroups/AzureVirtualDesktopResourceGroupCodeCrazy/providers/Microsoft.Compute/virtualMachines/CodeCrazy-0

###### Second thing I did at 7:49 AM CDT on 10-30-2021:
* Created Administrative Unit resource called "CodeCrazyAdministrativeUnit"
* Description: This is the Administrative Unit (AU) for the Code Crazy tenant.
* Assigned Roles as follows:
** Role "Authentication administrator"
*** Selected Items:
**** mmorelli@codecrazywin.com
**** rflickner@live.com
**** admin@AthenianStranger.onmicrosoft.com
** Role "Groups administrator"
*** Selected Items:
**** mmorelli@codecrazywin.com
**** rflickner@live.com
**** admin@AthenianStranger.onmicrosoft.com

### SECOND COMPLETE DELETE, NEW ACCOUNT, NEW EVERYTHING

1. Created `Microsoft 365 Group` called `team`.
2. Created a `Subscription` named `AzureMorelli`.
    2a. Created `Resource Group` called `CodeCrazyResourceGroup`.
        *Note: Used `East US` as region.
        * `Subscription ID`: **101400f7-b95a-49e7-b26e-9745ea04d6f7**
3. Modified `Tenant Name` to `Tenant Name` `Treemore`
4. Added a [custom domain](https://codecrazy.us) called `codecrazy.us`.
5. Created `Azure AD Domain Services` (including new `Resource Group` [see above]).
    5a. Added `Region` `East US`.
    5b. Made Azure AD Domain Services `SKU` "Enterprise" level.
6. Created **public** `Dashboard` called `CodeCrazyDashboard` and pinned `CodeCrazyResourceGroup` to it.
7. Pinned `Blade` "`All Resources`" to `CodeCrazyDashboard`.
8. Created `NSG` (**N**etwork **S**ecurity **G**roup) called `CodeCrazyNetworkSecurityGroup`
9. Created `VNET` in `Region` `East US` called `CodeCrazyVirtualNetwork`with address space `192.168.0.0/16` and `Subnet` called `CodeCrazySubnet` with address space `192.168.0.0/24`.
    9a. We associated the `VNET` with `Azure Active Directory` by clicking *Service Endpoints--Microsoft.AzureActiveDirectory*.
10. Created [Virtual] Network Interface Card (NIC) (a `NIC` used to be a physical device) called `CodeCrazyNetworkInterface`. Here are the paremeters:
    10a. Name: `CodeCrazyNetworkInterface`
    10b. Region: East US
    10c. Virtual Network: CodeCrazyVirtualNetwork
    10d. Subnet: CodeCrazyVirtualNetwork/CodeCrazySubnet
    10e. Private IP address assignment: Dynamic
    10f. NSG: CodeCrazyNetworkSecurityGroup
11. Created Public IP Address
    11a. Public IP: 104.45.177.66
    11b. DNS name: codecrazy.eastus.cloudapp.azure.com
    11c. Zone: Zone Redundant
    11d. Subscription ID: 101400f7-b95a-49e7-b26e-9745ea04d6f7
    11e. Zone: East US
    11f. SKU: Standard (there was no other option but Basic)
12. Associated Public IP with CodeCrazyNetworkInterface under CodeCrazyResourceGroup by clicking the little chainlink icon in the top right of the Public IP management interface window.
13. Added carlo.m.morelli@outlook.com as owner to all resources thus far created. Nevermind, I am Root.
14. Added Custom Domain Name under Azure Active Directory to point to [codecrazy.us](https://codecrazy.us).
    14a. TXT Record: MS=ms27104701
    14b. Alias = @
    14c. TTL = 3600

Created Azure Virtual Desktop and used the Wizard to do the following:

15. Created 3 Virtual Machines
    15a. Resource Group: CodeCrazyResourceGroup
    15b. Names:
        1. CCVM*
        2. CCVM*
        3. CCVM*
        * Note: * indicates that Azure will auto-number these VMs when created.
    15c. Properties:
        1. Region: East US
        2.
17. Create a `Host Pool` called `CodeCrazyHostPool`
    17a. Location: East US
    17b. Validation Environment: Yes
    17c. Host pool type: Pooled
    17d. Load balancing algorithm: Depth-first
    17e. Zone = 2
    17f. OU = Treemore
18. Created Workspace called `CodeCrazyWorkspace`

AVD Deployment Failed on 10-30-2021 at 9:45 PM CDT (2045)

* Operations ID: /subscriptions/101400f7-b95a-49e7-b26e-9745ea04d6f7/resourceGroups/CodeCrazyResourceGroup/providers/Microsoft.Resources/deployments/HostPool-c85e3026-3607-4213-8463-e471df9b607c-deployment/operations/DE3EB2195B54B3F1
* Operations Name: DE3EB2195B54B3F1
* Provisioning Operation: Create
* Provisioning State: Failed
* Timestamp: 10/30/2021, 9:42:22 PM
* Duration: 10 minutes 4 seconds
* Tracking ID: b9f04091-4042-4dca-953e-908345bdcb3c
* serviceRequestID: 975a98f3-b3d1-4d43-86c5-4dce6fe0b3f0
* Status: Conflict
* Type: Microsoft.Resources/deployments
* Resource ID: /subscriptions/101400f7-b95a-49e7-b26e-9745ea04d6f7/resourceGroups/CodeCrazyResourceGroup/providers/Microsoft.Resources/deployments/vmCreation-linkedTemplate-c85e3026-3607-4213-8463-e471df9b607c
* Resource: vmCreation-linkedTemplate-c85e3026-3607-4213-8463-e471df9b607c
* Deployment correlation ID: 8ce9e695-389f-4d3d-bfe4-b8355f0fc1d6

Attempts to Remedy Failure & Redeploy

* Removed custom domain codecrazy.us
* Removed OU
* Turned off validation environment (setting was true; changed to false)
* Attempted redeploy at 9:55 PM CDT
* **Redeploy Failed so I deleted everything**

New Attempt to Deploy AVD using Wizard at 10:09 PM CDT

* New redeploy: Start time:10/30/2021, 10:21:54 PM
* Correlation ID:ec1b0d55-6c0e-486e-8c38-87db548c763b
* HostPool-4b14a44c-59fb-4a17-bcb1-94f5ab4cc033-deployment
* Failed again.

## New Failure Notes for Ticket

Deployment Failed:

EXACT ERROR MESSAGE:
"{"code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see https://aka.ms/DeployOperations for usage details.","details":[{"code":"VMExtensionProvisioningError","message":"VM has reported a failure when processing extension 'joindomain'. Error message: \"Exception(s) occured while joining Domain 'codecrazy.us'\"\r\n\r\nMore information on troubleshooting is available at https://aka.ms/vmextensionwindowstroubleshoot "}]}"

### More Information

vmCreation-linkedTemplate-4b14a44c-59fb-4a17-bcb1-94f5ab4cc033

CCVM-0/joindomain | Status: Conflict

Operation ID: /subscriptions/101400f7-b95a-49e7-b26e-9745ea04d6f7/resourceGroups/CodeCrazyResourceGroup/providers/Microsoft.Resources/deployments/vmCreation-linkedTemplate-4b14a44c-59fb-4a17-bcb1-94f5ab4cc033/operations/13AD718BC2465292

Operation Name: 13AD718BC2465292

Provisioning State: Create

Provisioning State: Failed

Timestamp: 10/30/2021, 10:39:02 PM

Duration: 4 minutes 58 seconds

Tracking ID: 9435c8bf-ba97-44b7-a44b-d64e9e1db674

serviceRequestID: 9bf07371-5ae8-415c-bca9-7f6b60c0b8f8

Type: Microsoft.Compute/virtualMachines/extensions

Resource ID: /subscriptions/101400f7-b95a-49e7-b26e-9745ea04d6f7/resourceGroups/CodeCrazyResourceGroup/providers/Microsoft.Compute/virtualMachines/CCVM-0/extensions/joindomain

Resource: CCVM-0/joindomain

Deployment Correlation ID: 28e4005e-bdb4-457b-ace2-9481c5ff20b6

Status Message JSON output:

{
    "status": "Failed",
    "error": {
        "code": "VMExtensionProvisioningError",
        "message": "VM has reported a failure when processing extension 'joindomain'. Error message: \"Exception(s) occured while joining Domain 'codecrazy.us'\"\r\n\r\nMore information on troubleshooting is available at https://aka.ms/vmextensionwindowstroubleshoot "
    }
}

## POWERSHELL REDEPLOYMENT ATTEMPT

* I opened Cloud Shell and provisioned storage, then chose between Bash/PowerShell and chose PowerShell and then
* Typed this: `Get-Module -ListAvailable Az`
* According to [this site](https://docs.microsoft.com/en-us/azure/virtual-network/ip-services/create-public-ip-powershell?tabs=create-public-ip-standard%2Ccreate-public-ip-zonal%2Crouting-preference) my next command should be `Connect-AzAccount`
* None of this was neccesary because I was running from Azure's cloud shell
* Moving on
* Entered the following codeblock

```json
$ip = @{
    Name = 'myStandardPublicIP'
    ResourceGroupName = 'QuickStartCreateIP-rg'
    Location = 'eastus2'
    Sku = 'Standard'
    AllocationMethod = 'Static'
    IpAddressVersion = 'IPv4'
    Zone = 1,2,3
}
New-AzPublicIpAddress @ip
```

## Creating My Own Azure Virtual Desktop

* I decided to ditch the Wizard and do this manually.
* Using powershell

### Step 1: Create a host pool

## UPDATES AS OF FRIDAY, NOVEMBER 5, 2021

### FILE SHARE

1. At 6 AM CST (Texas/Chicago time) I spoke to a delightful Nigerian gentleman (MS Engineer) whose service scope was limited only to file shares.
2. He helped me configure the Network tab under the file share storage account to "All"; **THIS** *finally* permitted the local Azure File Explorer to view the folder and permit updates.
3. I uploaded a test MSIX package for an app ([MS VS Code x64 System Installer](https://code.visualstudio.com/sha/download?build=stable&os=win32-x64)) I'd created yesterday using the [MSIX Packaging Tool](https://docs.microsoft.com/en-us/windows/msix/packaging-tool/tool-overview).
    3a. The MSIX package was stored to my desktop (exact path: "C:\Users\mmore\Dropbox\PC (3)\Desktop\VSCODE.msix")
4. I navigated to the new application group I had created yesterday called "
    4a. The application group would not allow me to create or upload anything because it said there were no MSIX files stored in the Treemore-HostPool, so that's where I went next:
5. From the Azure online portal I navigated to All Resources>Treemore-HostPool
    5a. From within the Treemore-HostPool I went to the left navigation frame and selected Manage>MSIX packages
    5b. I clicked on the "+ Add" button.
    5c. A window popped up on the right side of the screen asking for an "MSIX image path"
        5c1. Hovering over the small (i) icon revealed this tooltip:

        ```txt
        "This is the path to a file share where the MSIX app attach container has been uploaded. VMs in the host must have read-only access on this path."
        ```
        
        5c2. I need to rememember to ensure IAM roles for the 3 VMs (TREE0; TREE1; & TREE2) all have read-only access using either `sudo chmod 444` (read-only command in Linux BASH; `attrib +r` in Elevated Windows CMD (probably not applicable here); or a similar set of commands in PowerShell--see below for PowerShell command to make read-only).
        
        5c3. **PowerShell Commands to Make Read-Only**
            5c3i. First, we must get the current attributes (remember, PS commands are `verb-noun` constructions):

            ```pwsh
            get-item -Path "c:\shared\readme.txt" | format-table name, attributes # (This is just an example showing how to fetch the current attributes of the filename)
            $file = Get-Item -Path "c:\shared\readme.txt" # (This assigns a variable named `file` to the path using the `$` prefix for variable assignments in PowerShell)
            $file.Attributes # (This fetches the current attributes of the variable `file`)
            $file.Attributes = @($file.Attributes,"ReadOnly") # (This command uses the assignment operator `=` and the `array operator` denoted by the "at symbol" `@` to *create a new array* which inherits all the attributes of the `$file` variable, adds the `ReadOnly` attribute, then **appends** the existing `$file` variable attributes with the new `@` array `ReadOnly` attributes (see ♕ for error and 🍕 to see how I solved it).
            ```

        5c4. Example from AdamTheAutomator
            * [AdamTheAutomator's Tutorial](https://adamtheautomator.com/how-to-make-a-file-read-only/) showing how to assign read-only access to a file he created called `readme.txt`:
        
           * Note: I would do the same for my `VSCODE.msix` package
           * ♕: I realized later I *first* needed to **convert** the `MSIX` package to either a `VHD` or `CMI` file *but I did not know this at the time* so I am posting this because *this was the timeline* of how I *tried and failed*, then *finally* learned how to do it **correctly**:
            
                ```
                PS C:\> $file = get-item -Path "c:\shared\readme.txt"
                PS C:\> $file.Attributes # Just returned Archive as only attribute in Adam's code example
                PS C:\> $file.Attributes = @($file.Attributes,"ReadOnly") # Assigns new array to `$file` existing `Attributes` (**appends** to existing attributes) and makes variable `ReadOnly`.
                PS C:\> get-item -Path "c:\shared\readme.txt" | format-table name, attributes # This PS command fetches/returns newly-added `@ array` attributes assigned to `$file` variable, formats a simple table with two columns with headers `Name` and `Attributes`. The output was a simple table showing that `readme.txt` had been assigned the attributes `ReadOnly` and `Archive`.
                ```
            
        * 🍕: This whole process didn't work because I had not yet converted my `MSIX` file to either VHD, VHDx, and CIM extensions (see ♝ for command used to create and ♜ for CIM extension example) since those are the only supported extensions in the Azure Portal's Host Pool MSIX Packages `Add MSIX Package` image path field. Now we move on to converting our `VSCODE.MSIX` package to have one of the supported extensions:

    5d. **Converting MSIX package to have VHD, VHDx, or CIM Extension** (see 🍕 and ♕ above for reasons why I had to do this)
        5d1. The process of converting or adding to an MSIX package either a VHD, VHDx, or CIM extension **required me to install the MSIXMGR tool** as shown in [this Microsoft Tech Community Tutorial](https://techcommunity.microsoft.com/t5/azure-virtual-desktop/simplify-msix-image-creation-with-the-msixmgr-tool/m-p/2118585).
    5d2. To install the `msixmgr` tool I had to complete the following steps:
            5d2i. [Download the MSIXMGR from Microsoft](https://aka.ms/msixmgr)
            5d2ii. Unzip MSIXMGR.zip into a local folder
            5d2iii. Open Command prompt (CMD) in elevated mode
            5d2iv. Navigate to the local folder from the second step
            5d2v. Run the following CMD command:
                * MSIXMGR Code Template

                   ```cmd
                   msixmgr.exe -Unpack -packagePath <path to package> -destination <output folder> [-applyacls] [-create] [-vhdSize <size in MB>] [-filetype <CIM | VHD | VHDX>] [-rootDirectory <rootDirectory>]
                    ```

                * ♝**MDIX to VHDx Extension Example**:
                
                    ```cmd
                    msixmgr.exe -Unpack -packagePath "C:\Users\ssa\Desktop\FileZillaChanged_3.51.1.0_x64__81q6ced8g4aa0.msix" -destination "c:\temp\FileZillaChanged.vhdx" -applyacls -create -vhdSize 200 -filetype "vhdx" -rootDirectory apps
                    ```
            
            5d2vi. Navigate to the destination folder and confirm that an MSIX image (.VHDX) was created
           
            ♜: **MDIX to CIM Extension Example**
                
                ```
                msixmgr.exe -Unpack -packagePath "C:\Users\ssa\Desktop\FileZillaChanged_3.51.1.0_x64__81q6ced8g4aa0.msix" -destination "c:\temp\FileZillaChanged.cim" -applyacls -create -vhdSize 200 -filetype "cim" -rootDirectory apps
                ```

## Error

1. Running the above returned an error indicating `msixmgr.exe` was not installed so I [downloaded it from Mirosoft](https://github.com/microsoft/msix-packaging/releases) and ran the MSI file to install it.
2. Unfortunately, the same error was returned, namely, "'msixmgr.exe' is not recognized as an internal or external command, operable program or batch file."
    * Here is the exact script I an in an elevated CMD:

    ```pwsh
    msixmgr.exe -Unpack -packagePath "C:\Users\mmore\Dropbox\PC (3)\Downloads\msixmgr (2)\x86\en-US\msixmgr.exe.mui" -destination "C:\Users\mmore\Dropbox\LAMAR CISD\GRHS\CS\Treemore\VSCODEMSIX\VSCODEVHDCIM\vscodevhdxtype.vhdx" -applyacls -create -filetype "vhdx" -rootDirectory apps
    ```

3. So, we created another MSIX package for VS Code and will now re-attempt the above prompt with the following exact command:

"C:\Users\mmore\Dropbox\LAMAR CISD\GRHS\CS\Treemore\VSCODEMSIX\vscodemsixpkg.msix"

    ```pwsh
    msixmgr.exe -Unpack -packagePath "C:\Users\mmore\Dropbox\PC (3)\Downloads\msixmgr (2)\x86\en-US\msixmgr.exe.mui" -destination "C:\Users\mmore\Dropbox\LAMAR CISD\GRHS\CS\Treemore\VSCODEMSIX\VSCODEVHDCIM\vscodevhdxtype.vhdx" -applyacls -create -filetype "vhdx" -rootDirectory apps
    ```

### Amit Session on 11/5/2021 around 3 PM

1. Sent me link: <https://christiaanbrinkhoff.com/2020/12/02/the-future-of-application-virtualization-learn-here-how-to-create-and-configure-msix-app-attach-packages-containers-on-windows-10-enterprise-multi-and-single-session-build-2004-and-higher-for-win/>
2. Amit, very helpful guy, mentioned there was a PS command that might work since our CMD attempts keep failing, so we are trying this command:

    ```pwsh
    New-VHD -SizeBytes 2048MB -Path "C:\Users\mmore\Dropbox\LAMAR CISD\GRHS\CS\Treemore\VSCODEMSIX\vscodevhd.vhd" -Dynamic -Confirm:$false
    ```

3. It worked! The file path locally is "C:\Users\mmore\Dropbox\LAMAR CISD\GRHS\CS\Treemore\VSCODEMSIX\vscodevhd.vhd"
4. Now I will push to Azure through the local file management client Microsoft Azure File Explorer.
5. Here is the Azure command for PS to the same thing: $env:AZCOPY_CRED_TYPE = "Anonymous";
./azcopy.exe copy "C:\Users\mmore\Dropbox\LAMAR CISD\GRHS\CS\Treemore\VSCODEMSIX\vscodevhd.vhd" "https://treemorefileshare.file.core.windows.net/userappfileshare/vscodevhd.vhd?se=2021-12-05T20%3A18%3A22Z&sp=rwl&sv=2018-03-28&sr=s&sig=DZF2T9AZk8k%2Bhhxz0n1dtRSjbuHkP7VcB12rheH42fk%3D" --overwrite=prompt --from-to=LocalFile --follow-symlinks --put-md5 --follow-symlinks --preserve-smb-info=false --recursive --trusted-microsoft-suffixes= --log-level=INFO;
$env:AZCOPY_CRED_TYPE = "";

6. After uploading the VHD file, go to the file share storage location of the VHD file and click the elipses "..." and copy the URL (https://treemorefileshare.file.core.windows.net/userappfileshare/vscodevhd.vhd), then go to Host Pool and click on MSIX Packages, then paste the URL to the VHD BUT make sure you change all the forward slashes to backslashes (this is mentioned nowhere--thank you Amit!). So the correct file path will be: "\\treemorefileshare.file.core.windows.net\userappfileshare\vscodevhd.vhd"
    * Note: Amit says we may OMIT the HTTPS part and just include the file path.
    * Begin the filepath (after deleting the HTTPs stuff) with two backslashes "\\" followed by the path.
7. That didn't work, here's the error:

    ```json
    {"code":"400","message":"ActivityId: 6b92812a-8b36-4d17-83e6-f9d34ff24556 Error: The MSIX Application metadata expand request failed on all Session Hosts that it was sent to. Session Host: TREE-2, Error: Virtual disk not found at ≤\\\\treemorefileshare.file.core.windows.net\\userappfileshare\\vscodevhd.vhd≥.Session Host: TREE-1, Error: Virtual disk not found at ≤\\\\treemorefileshare.file.core.windows.net\\userappfileshare\\vscodevhd.vhd≥.Session Host: TREE-0, Error: Virtual disk not found at ≤\\\\treemorefileshare.file.core.windows.net\\userappfileshare\\vscodevhd.vhd≥."}
    ```

    * Note: VHD stands for Virtual ____ Disk
    * Created PublicIP for TREE0 VM: 20.119.65.41 so we could RDP to it.
    * That did the trick--but only after I remembered to go into

8. Created new support ticket number 2111050040007156

    ```txt
    Summary: Need NSG & domain controller to sync all users to Azure AD + same for Host Pool VMs + VHD Link Issue
    
    Product: Azure/Azure Dedicated Host/Configuration Issues on Dedicated Host/Host issues
    Azure Subscription: Azure subscription 1
    Azure Subscription ID: f31ae3bb-1685-4331-975d-fbb97598b68b
    
    Details: Current Host Pool was setup with Azure Virtual Active Directory instead of Azure AD; now I am trying to link an MSIX-rendered VHD file through a fileshare and cannot make the connection...after several hours of troubleshooting the tech Amit suggested the issue may rest at the domain controller level. No limitations for AD Join service wherein we cannot deploy MS App Attach; in other words, I cannot communicate across my network between my resources. Problem start date and time; Thu, Nov 4, 2021, 12:00 AM CDT.
    ```

## Surya (technician number 28 in the last the 3 weeks) from MS Networking Team Begins at 5:40 PM CST

## Andy from Networking called at 5:50 PM CST
1. Andy is going to speak to his team administrator and help to solidify the scope of the issue and ramify **networking** as the central scope rather than the presently set scope which is limited to Azure Virtual Desktop. 

## Notes

* `SKU` means pricing tier (learn more [here](https://docs.microsoft.com/en-us/azure/search/search-sku-tier)).
