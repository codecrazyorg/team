# TROUBLESHOOTING USER ACCESS ERROR TO WVD/AVD

## Actions Taken to Resolve AVD/WVD User/Group Session Error "Your do not have access to this resource"

## First thing I did at 7:45 AM CDT on 10-30-2021
* Created IAM Role Assignment to AVD/WVD Virtual Machine Code-Crazy-0 granting role Virtual Machine User Login to Group "Programmers". 
* Programmers has type "Security Group" and Object ID of 
ed61d18b-2055-461d-b619-f9110ad49971 and is type "Group".
* The scope of this Role Assignment is: /subscriptions/b520aa79-4f34-44f6-af71-8b5711f5d0e6/resourceGroups/AzureVirtualDesktopResourceGroupCodeCrazy/providers/Microsoft.Compute/virtualMachines/CodeCrazy-0

## Second thing I did at 7:49 AM CDT on 10-30-2021:
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
