Procedure
Part A: Creating an EC2 Instance

Step 1: Open the EC2 service
Log in to your AWS account. On the AWS Management Console, click Services and choose EC2 from the drop-down menu.

Step 2: Launch an instance
Click Launch Instance. This opens the launch page where the instance is configured. Enter a name for the instance.

Step 3: Select an AMI (Amazon Machine Image)
Choose the operating system you need from the available AMIs (e.g., Amazon Linux, Ubuntu, Windows).

Step 4: Choose the instance type and key pair

The default instance type is t2.micro, which is Free Tier eligible. It specifies the number of CPUs and the amount of memory.
Do not select any other type, as it may lead to charges.
Create or select a key pair (.pem file) and keep it safe. It is needed for SSH access.

Step 5: Configure network and storage
Keep the network settings at their defaults unless changes are required. Free Tier eligible accounts get up to 30 GB of EBS storage. Keep the default.

Step 6: Launch
Check that all selected options are Free Tier eligible, then click Launch Instance. The instance is now created.

Part B: Connecting to the Instance via Terminal Using an SSH Key

Step 1: Select the instance you want to connect to and click the Connect button at the top of the instance page.

Step 2: Copy the SSH command shown in the SSH client tab. It uses your key pair to connect to the EC2 instance.

Step 3: Open a terminal, go to the folder where your .pem file is saved, and paste the copied command.



