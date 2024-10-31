**Insert S3 csv file content to RDS MySQL using lambda function**

**1 Create an RDS MySQL Instance:**

Navigate to the RDS service and create a new database instance.

Select MySQL as the engine and enable public access.

**2 Set Up a Lambda Function:**

Go to the Lambda service and click on Create function.

Choose Author from scratch.

Function name: s3-rds-mysql

Runtime: Python 3.10

Under Permissions, select the default role and attach the S3 Object Read Only permission to the Lambda function.

Click on Create function.

**3 Prepare the Lambda Function Code:**

Open a terminal and create a directory for your code:

bash

**Copy code**

    -mkdir /home/RDSCode
    -cd /home/RDSCode

Install the required library:

bash

**Copy code**

    -pip install -t /home/RDSCode pymysql

Create a new Python file:

bash

**Copy code**

    -vi lambda_function.py

Copy the entire code from this GitHub repository.

      -https://github.com/prabhakar2020/insert_s3_csv_file_content_to_mysql_using_lambda
      
**4 Package and Upload the Code:**

Zip the directory:

bash

**Copy code**
    zip -r directoryName.zip .

Upload the zipped file to the Lambda function. Click on the Upload button and select the zip file.

**5 Configure Database Connection:**

Copy your RDS endpoint and insert it into the Python code for the connection:

python

**Copy code**

    -rds_endpoint = "database-test.c5kay8g0u99c.us-east-1.rds.amazonaws.com"
    -username = "admin"
    -password = "admin12345"  # RDS MySQL password
    -db_name = "employee"

Save the changes by clicking on Deploy.

**6 Set Up S3 Bucket Event Notification:**

Create a new bucket in S3.

Navigate to the bucket, go to Properties, and click on Event Notifications.

Click on Create event notification:

Event name: [Your Event Name]

Event types: Select All object create events

Destination type: Choose Lambda function

Destination: Select the Lambda function s3-RDS-mysql.

**7 Monitor Logs:**

You can check the logs in CloudWatch under Log groups. Click on /aws/lambda/s3-RDS-mysql, then Log streams to view the current logs.

**8 Verify Data Insertion:**

Access your RDS instance using the following command:

bash

**Copy code**

    -mysql -h database-test.c5kay8g0u99c.us-east-1.rds.amazonaws.com -u admin -p


This process will set up a Lambda function that automatically inserts CSV file content from S3 into your RDS MySQL database whenever a new file is uploaded.

