**Using the AWS Management Console**

Navigate to EC2: In the console dashboard, type EC2 in the search bar and select it. Once on the EC2 page, click Instances in the sidebar, then select Launch Instances.

**Configure Your Instance:**

Instance Name: Provide the name you’d like for your instance.

Application and OS Images (AMI): Choose your preferred operating system.

Instance Type: Select an instance type, such as t2.micro (eligible for free tier usage).

Key Pair: Choose or create a Key Pair for secure access to your instance.

Security Group: Use the default security group or configure as needed.

Launch Instance: Review your configurations and click Launch Instance to deploy.

Using the AWS CLI
Configure AWS CLI: Start by setting up your AWS CLI credentials using:

**bash Copy code**

      -aws configure
   
      AWS Access Key ID: Enter your Access Key.
      
      AWS Secret Access Key: Enter your Secret Key.
      
      Default Region Name: For example, us-east-1.

Default Output Format: Choose json or another format if preferred.

Verify CLI Configuration: Test your CLI setup with:

**bash Copy code**
    -aws sts get-caller-identity

      Expected Output:
      
      json
      
      Copy code
      {
         "Account": "123456",
         "Arn": "arn:aws:sts::123456:assumed-role/role-name/role-session-name",
         "UserId": "AR#####:#####"
      }

Launch EC2 Instance via CLI: Use the following command, replacing <Key-Pair-Name> with your Key Pair name:

bash

Copy code

      -aws ec2 run-instances --image-id ami-08e4e35cccc6189f4 --count 1 --instance-type t2.micro --key-name <Key-Pair-Name> --security-groups default

This will initiate the creation of an EC2 instance based on your specifications.






