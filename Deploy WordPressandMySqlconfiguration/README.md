**Deploying WordPress and MySQL on an EC2 Instance via Console/CLI**

1. Launch EC2 Instance

Use the following CLI command to launch an instance:
bash
**Copy code**

    -aws ec2 run-instances --image-id ami-0149b2da6ceec4bb0 --count 1 --instance-type t2.micro --key-name newkeypair --security-groups default

Configure the instance security group to allow SSH (port 22) and HTTP (port 80):
bash
**Copy code**

    -aws ec2 authorize-security-group-ingress --group-id sg-03a50b08d049283de --ip-permissions IpProtocol=tcp,FromPort=22,ToPort=22,IpRanges="[{CidrIp=0.0.0.0/0}]"
    -aws ec2 authorize-security-group-ingress --group-id sg-03a50b08d049283de --ip-permissions IpProtocol=tcp,FromPort=80,ToPort=80,IpRanges="[{CidrIp=0.0.0.0/0}]"

2. Connect to the EC2 Instance and Update Packages
   
Run:
bash

**Copy code**

    -sudo apt-get update

3. Install Apache, MySQL, and PHP Using Tasksel

Install Tasksel:
bash
**Copy code**

    -sudo apt-get install tasksel

Launch Tasksel and select the LAMP package (includes Apache, MySQL, PHP):
bash

**Copy code**

    -sudo tasksel

Within Tasksel, use the down arrow to navigate to LAMP, press Space to select it, then Tab to the OK button, and press Enter.

4. Verify Apache Installation

Enter your instance’s public IP in a browser to confirm Apache is running.

5. Start and Configure MySQL

Start MySQL and configure it:

bash
**Copy code**

    -sudo service mysql start
    -sudo mysql -u root -p

Once in MySQL, execute the following commands:
sql
**Copy code**

    -CREATE USER 'ubuntu'@'localhost' IDENTIFIED BY 'password';
    -CREATE DATABASE wordpress;
    -GRANT ALL PRIVILEGES ON wordpress.* TO "ubuntu"@"localhost";
    -GRANT PROCESS ON *.* TO "ubuntu"@"localhost";

Exit MySQL by pressing Ctrl + D.
6. Download and Configure WordPress
Download and extract WordPress:
bash
**Copy code**

    -wget https://wordpress.org/latest.tar.gz
    -tar xzf latest.tar.gz
    -cd wordpress

Copy and edit the WordPress configuration:
bash
**Copy code**

    -cp wp-config-sample.php wp-config.php
    -sudo nano wp-config.php

Update wp-config.php with database details:
php

**Copy code**

    -define( 'DB_NAME', 'wordpress' );
    -define( 'DB_USER', 'ubuntu' );
    -define( 'DB_PASSWORD', 'password' );

7. Deploy WordPress on Apache
Copy WordPress files to Apache’s root directory:
bash
**Copy code**

    -sudo cp -r * /var/www/html
    -sudo cp -r wp-admin /var/www/html
    -sudo cp -r wp-content /var/www/html
    -sudo cp -r wp-includes /var/www/html

Remove the default index.html:
bash
**Copy code**

    -cd /var/www/html
    -sudo rm index.html

Restart Apache:
bash
**Copy code**

    -sudo service apache2 restart

8. Verify WordPress Deployment
   
Retrieve the public IP of your instance from the AWS Console and enter it in your browser. Your WordPress site should be accessible at:
vbnet
**Copy code**
http://<public IP of your EC2 instance>
