**DB Migrations Mysql to Mysql**

**Step 1: Configure the Source Database Instance (mySourceDatabase)**

Navigate to: AWS RDS service.

Create Database: Select the Standard database creation method.

Engine: Choose MySQL.

Templates: Choose Free Tier.

DB Instance Identifier: Enter mySourceDatabase.

Credentials:
Username: admin
Password: admin12345

DB Instance Class: Select Burstable classes - db.t3.micro.

Storage Autoscaling: Disable.

Public Access: Enable.

Additional Configuration:

Database Options: Initial database name set to myDatabase.

Backup: Leave unselected.

Encryption: Leave unselected.

**Step 2: Configure the Target Database Instance (myTargetDatabase)**

Navigate to: AWS RDS service.

Create Database: Select Standard.

Engine: Choose MySQL.

Templates: Choose Free Tier.

DB Instance Identifier: Enter myTargetDatabase.

Credentials:

Username: admin

Password: admin12345

DB Instance Class: Select db.t3.micro.

Storage Autoscaling: Disable.

Public Access: Enable.

Database Port: Set to 3306.

Database Options: Leave initial database name field blank.

Backup: Leave unselected.

Encryption: Leave unselected.
**Step 3: Set Up AWS DMS (Database Migration Service)**

Create Replication Instance:

Name: myReplica

Resource Name: DemoARN

Instance Class: dms.t3.micro

High Availability: Select Dev or Test.

Storage: Set to 20 GB.

**Step 4: Connect to the Source Database**

Get the Endpoint: Retrieve the endpoint of the mySourceDatabase instance from RDS.

Connect via CLI:

bash

**Copy code**
    
    -mysql -h mysourcedatabase.c5kay8g0u99c.us-east-1.rds.amazonaws.com -u admin -p admin12345

Adjust Security Settings if connection issues arise:

Go to Connection and Security for the database instance.

Edit VPC Security Groups, add an inbound rule for All Traffic with Source: Anywhere (IPv4).

Create and Insert Data:

sql

**Copy code**
    
    -USE myDatabase;
    -CREATE TABLE tablename (...);
    -INSERT INTO tablename (...) VALUES (...);


**Step 5: Set Up Endpoints in DMS for Source and Target Databases**

Source Endpoint:

Endpoint Identifier: mySource

Resource Name: DemoSourceARN

Engine: MySQL

Access Info:

Server Name: Use mySourceDatabase endpoint.

Port: Set to 3306.

Username: admin

Password: admin12345

Target Endpoint:

Endpoint Identifier: myTarget

Resource Name: DemoTargetARN

Engine: MySQL

Access Info:

Server Name: Use myTargetDatabase endpoint.

Port: 3306

Username: admin

Password: admin12345

**Step 6: Create and Configure Database Migration Task**

Task Identifier: myMigrationTask

Resource Name: DemoMigrationsARN

Replication Instance: Select myReplica.

Source Database Endpoint: mySource

Target Database Endpoint: myTarget

Migration Type: Select Migrate Existing Data.

Selection Rules: Add new selection rule:

Schema: Specify the schema to migrate.

Pre-migration Assessment: Choose No.

Create Task.

This configuration completes the setup for migrating a MySQL database from one RDS instance to another using AWS DMS.

