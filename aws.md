# Setting Up My First AWS Workspace

* Today I spoke with an AWS technician about how best to mimic the infrastructure I'd created on Azure and he suggested `AWS Workspaces` and said `VS Code` could *easily* be implemented there.

## Installation

### Today (November 6, 2021)

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
  * Now what?
