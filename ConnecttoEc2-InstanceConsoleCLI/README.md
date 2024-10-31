**Connect to Ec2-Instance Console/ CLI**

Connect via AWS Console

Launch EC2 Instance: First, create an EC2 instance using either the console or CLI.

Instance Connection:

Go to your Instances list and click on the Instance ID.

On the instance details page, select Connect (found on the right side).

Under EC2 Instance Connect, click Connect to open the instance shell in your browser.

SSH Client Connection:

Alternatively, connect via SSH by using the command provided in the SSH client section:

bash
**Copy code**
    -ssh -i "newkeypair.pem" ec2-user@ec2-52-6-251-26.compute-1.amazonaws.com
    
Connect via CLI
Run SSH Command: Use the command provided in the SSH client section to connect via CLI:

bash
**Copy code**
    -ssh -i "newkeypair.pem" ec2-user@ec2-52-6-251-26.compute-1.amazonaws.com
    
Note: Ensure that the .pem file is located in the same directory where you execute this command.
Troubleshooting Connectivity Issues
If you are unable to connect, you may need to adjust inbound rules:
Modify Security Group Inbound Rules:
Add an ingress rule for SSH to the instance’s security group. Replace the security group ID as needed:

bash
**Copy code**
    -aws ec2 authorize-security-group-ingress --group-id "sg-03a50b08d049283de" --protocol tcp --port 22 --cidr "0.0.0.0/0"
    
Re-create Instance:
If necessary, terminate the existing instance and launch a new one using:

bash
**Copy code**
    -aws ec2 run-instances --image-id ami-08e4e35cccc6189f4 --count 1 --instance-type t2.micro --key-name <Key-Pair-Name> --security-groups default

Reconnect:
Use the updated SSH command from the SSH client section on the Instance Dashboard:

bash
**Copy code**
    -ssh -i "newkeypair.pem" ec2-user@ec2-52-6-251-26.compute-1.amazonaws.com
    
This ensures a secure and seamless connection to your EC2 instance.
