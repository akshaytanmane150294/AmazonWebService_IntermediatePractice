**Creating an IAM User on AWS**

  In the AWS console, search for "IAM" in the search bar and select "Users" from the menu on the left.
  
  Click the "Create User" button on the top right. Provide a username and check the box for "I want to create an IAM user".
  
  Select Custom password, enter your password, and click Next.
  
  On the Permissions page, select Attach policies directly. Search for "AdministratorAccess", check the AdministratorAccess policy, and click Next.
  
  Proceed to the next page without changes, and click Create User.
  
  Important: Once the user is created, download the CSV file containing user credentials for safekeeping.
  
  Optional: Enabling Multi-Factor Authentication (MFA)

**To enable MFA, go to the Users list and click on the desired username.**

  Under Console Access, click Enabled without MFA to enable MFA.
  
  On the MFA setup page, provide a Device name and proceed.
  
  Download and open the Google Authenticator app on your mobile device.
  
  Display the QR code in AWS, scan it with Google Authenticator, and complete the setup.
  
  Verify MFA by logging in with your new IAM user credentials.
