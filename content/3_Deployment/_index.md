---
title: "Deployment"
chapter: false
menuTitle: "Deployment"
weight: 30
---

Once the prerequisites have been satisfied proceed with the deployment steps below.

1.  To download the template, you can either clone the repo with the git command below, or [**download**](https://github.com/FortinetCloudCSE/fortigate-aws-standalone-cloudformation) the repo as a ZIP archive.  The template is in the **/cloudformation folder**

```
git clone https://github.com/FortinetCloudCSE/fortigate-aws-standalone-cloudformation.git
```

![](get1.png)

2.  Login to your AWS account.  In the AWS services page under All Services > Management Tools, select CloudFormation.

	![](deploy1.png)

3.  Select Create Stack then select with new resources.

	![](deploy2.png)

4.  On the Select Template page, under the Choose a Template section select Upload a template to Amazon S3 and browse to your local copy of the chosen deployment template.

	![](deploy3.png)

5.  On the Specify Details page, you will be prompted for a stack name and parameters for the deployment.  We are using the **'FortiGate_Standalone_ExistingVPC.template.json'** template which deploys a FGT into an existing VPC's public & private subnets and gives options for configuring the instance settings.

{{< notice warning >}} 
The public subnet should have a default route to an Internet Gateway or bootstrapping the config and license of the FGT will fail.

After deployment, you will need to create a route for the private subnet referencing ENI1/port2 of the FGT for routing non NAT'd inbound and outbound initiated traffic.
{{< /notice >}}

![](deploy4.png)

6.  In the FortiGate Instance Configuration parameters section, we have selected an Instance Type and Key Pair to use for the FortiGates, chose to encrypt both OS and Log disks, as well as BYOL licensing.  Notice we are prompted for the licensing type which we are going with tokens.  In our case we do not need to fill out the InitS3Bucket parameter.

7.  In the Interface IP Configuration for the FortiGate parameters section, we are going with the defaults in this example as the subnet addressing matches.  These IPs will be the primary IPs assigned to the FortiGate ENIs.

8.  On the Options page, you can scroll to the bottom and select Next.

9.  On the Review page, scroll down to the capabilities section.  As the template will create IAM resources, you need to acknowledge this by checking the box next to ‘I acknowledge that AWS CloudFormation might create IAM resources’ and then click Submit.

	![](deploy5.png)

10.  On the main AWS CloudFormation console, you will now see your stack being created.  You can monitor the progress by selecting your stack and then select the Events tab.

![](deploy6.png)

11.  Once the stack creation has completed successfully, select the Outputs tab to get the login information for the FortiGate instances and cluster.

![](deploy7.png)

12.  This concludes the template deployment example.
