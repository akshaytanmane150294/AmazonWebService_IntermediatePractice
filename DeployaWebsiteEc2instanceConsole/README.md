**Deploying a Website on an EC2 Instance via Console**

Launch EC2 Instance:

In the EC2 Dashboard, create a new instance, specifying a name and choosing Ubuntu as the operating system.

Select your Key Pair and under Network Settings, add a new security rule:

Keep the default SSH rule (TCP, port 22).

Click Add Security Group Rule, choose HTTP to allow web traffic, and set the source to 0.0.0.0/0.

Click Launch.

Connect to Your Instance via SSH:

Connect to the instance using the following SSH command:

bash

**Copy code**

    -ssh -i "newkeypair.pem" ubuntu@ec2-34-238-240-232.compute-1.amazonaws.com


Install Apache Web Server:
Run the following commands:
bash

**Copy code**

    -sudo apt-get update
    -sudo apt install apache2


Verify Apache is running:

bash

**Copy code**

    -sudo systemctl status apache2


If Apache is not running, start it:

bash

**Copy code**

    -sudo systemctl start apache2


To stop the server:

bash

**Copy code**

    -sudo systemctl stop apache2


Update the Web Page:

Go to the web server’s default HTML path:

bash

**Copy code**

    -cd /var/www/html


Update or create an index.html file here.

Verify Your Website:

Open your browser and go to:

http://{yourPublicIp}/

http://{yourPublicIp}/var/www/html/index.html

Deploying a Website on EC2 Using CLI
Launch EC2 Instance:
Run the following command to create an instance via CLI:

bash

**Copy code**

    -aws ec2 run-instances --image-id ami-0149b2da6ceec4bb0 --count 1 --instance-type t2.micro --key-name newkeypair --security-groups default


Configure Security Group:
Add SSH and HTTP rules with these commands:
bash

**Copy code**

    -aws ec2 authorize-security-group-ingress --group-id sg-03a50b08d049283de --ip-permissions IpProtocol=tcp,FromPort=22,ToPort=22,IpRanges="[{CidrIp=0.0.0.0/0}]"
    -aws ec2 authorize-security-group-ingress --group-id sg-03a50b08d049283de --ip-permissions IpProtocol=tcp,FromPort=80,ToPort=80,IpRanges="[{CidrIp=0.0.0.0/0}]"


Connect via SSH:
Use SSH to connect:
bash

**Copy code**

    -ssh -i "newkeypair.pem" ubuntu@ec2-34-238-240-232.compute-1.amazonaws.com


Install and Configure Apache:

Follow the instructions from Steps 3 and 4 above to set up and test the Apache server.

This completes the website deployment on your EC2 instance using either the Console or CLI.
