# VM Migration from Aws to Gcp

## Prerequisites

Boath AWS and GCP Accounts required.

First make sure you must have an EC2 instance with small application installed in it.

here, In EC2 instance apache2 is installed.

![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(124).png)

## Cloudendure Configuration

Cloudendure is used for VM migration. It is agent base migration tool so you have to install an agent in VM that will be migrated. 

* Go to Compute Engine in GCP Concole.

* Click on Import VM.

* Once you click on that you find the bellow screen

![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(83).png)

* Click on Cloudendure

* Login in this using you GCP account

* Click on create new project or you can use default project.

```Note: CLoudendure and GCP projects are diffrent from each other so you can set any name for porject it will not effect your GCP account```
  
![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(104).png)

* Enter your GCP project id

* Enter Service Account private key in ```Google Cloud Platform JSON Private Key```

  * You can get that from GCP Console -> APIs & Services -> Credentials
  
  ![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(105).png)
  
  * Create Credentials for Service Account
  
  ![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(106).png)
  
  * Select Compute Engine default service account
  
  ![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(108).png)
  
  * After creating credentials it will automatically download JSON file. Open that JSON file in Cloudendure Console for private key
  
  ![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(109).png)

* Next enter details to where you want to create you Compute Engine

![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(110).png)

```## NOTE : Here is one option Use VPN or Cloud interconnect. If we not enable this then it use public internet to migarte our VM, so it slow down the process of migration. So we can use VPN connected with AWS VPC via tunnel then it will do secure and fast migration.  ``` 

![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(111).png)

* Setup is completed

* Install Cloudendure agent on AWS EC2 using givne configuration.

    Since we using Linux instance on EC2 so we use linux configration.

![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(112).png)

* Downloading agent in EC2 instance 

![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(113).png)

* Excute using next command to verfiy the cloudendure in EC2

![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(114).png)

* Back to the Cloudendure console you can see the process of data replication has just started. It take 25-30 miniutes to replicate beacuse we using public internet for migrating the VM.

![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(115).png)

* Once Replication is completed you have to create Blueprint for configration of machine of GCP

![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(117).png)

* Now click on ```LAUNCH TARGET MACHINE``` you will see there is 2 option:

  1. Test Mode : When you launch target machine in test mode you can do countinus data replication from AWS to GCP.
  
  ![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(118).png)
  
  2. Cutover : In this mode you have no further contact with your AWS instance.
  
  ![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(119).png)

* Here we launch machine in Test mode.

![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(120).png)

* You can see progress in Job Progress

![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(121).png)

* After a few minutes you can see 2 instance is launched in your GCP consel

![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(122).png)

the one is our acutal VM which is migrated from AWS and another one is Cloudendure replicator, since we are doing in Test mode so it create replicator, if you launch in cutover mode you will not find that instance.

* This is migrated VM on GCP

![](https://github.com/Petabytz/GCP-Projects/blob/master/VM%20Migration/AWS%20to%20GCP%20by%20cloudendure/Screenshot%20(123).png)

* If you want to ssh in GCP instance you can not direclty do that by clicking on ```ssh button```, you have to use PUTTY or SSH client to connect to that instance using same ssh key which is genrated form AWS EC2 instance.
