**Code commit and Code build and S3 Artifacts**


**1) Setting Up CodeCommit**

First, navigate to the IAM service, go to Users, and select Security Credentials.

Under HTTPS Git credentials for AWS CodeCommit, generate a password, download it locally, and grant all necessary CodeCommit permissions to the user, such as AWSCodeCommitFullAccess and AWSCodeCommitPowerUser.

If needed, create a custom policy under Policies and attach it to the user for further access management.

Next, go to CodeCommit, create a new repository by providing a name and an optional description, then select Create.

Copy the HTTP clone URL of the repository for local cloning.

After setting up the repository locally, add an index.html file to the project.

Push this file to CodeCommit using the following commands:

bash

**Copy code**
    
    -git add .
    -git commit -m "added HTML file"
    -git push origin master
    
**2 )  Setting Up CodeBuild**

Go to the CodeBuild service and select Create Build Project.

Assign a project name.

Under Source, select Source Provider as CodeCommit, and select your repository (e.g., demoapp).

Branch: master (or your desired branch)

Under Environment, select:

Environment Image: Managed Image

Operating System: Ubuntu

Runtime: Standard

Image: aws/codebuild/standard:6.0

Environment Type: Linux

Service Role: New service role (provide a name)

Under Build Specifications, choose Buildspec File.

Within the project directory, create a buildspec.yml file with the following content:

yaml

**Copy code**

      -version: 0.2
      phases:
        install:
          commands:
            - echo Installing NGINX
            - sudo apt-get update
            - sudo apt-get install nginx -y
        build:
          commands:
            - echo Build started on `date`
            - cp index.html /var/www/html/
        post_build:
          commands:
            - echo Configuring NGINX
            - echo Creating ZIP file
            - zip -r buildspec-output.zip ./*
      artifacts:
        files:
          - buildspec-output.zip
        discard-paths: yes
        base-directory: .
        name: buildspec-output.zip
        override-artifact-name: true

Commit and push the buildspec.yml file to CodeCommit.

Click on Create Build to initialize the build.

**3)  Storing Artifacts in S3**

Open your build project, select Edit, and go to the Artifacts section.

Set Type to S3.

Go to S3 and create a bucket. Assign a bucket name (e.g., your-bucket-name).

Specify the artifact name within Name as a folder (e.g., buildspecs-folder).

Update the artifact configuration.

Once the build completes, the artifact (ZIP file) will be available in the S3 bucket.

Download and unzip the file on your local machine with:

bash

**Copy code**

    -unzip buildspec-output.zip

The unzipped content will contain the index.html, appspec.yml, buildspec.yml, and script files from your project.

