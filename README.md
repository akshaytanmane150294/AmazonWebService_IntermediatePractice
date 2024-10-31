**AWS Billing and CloudWatch Alarm Setup**

    -This document provides step-by-step guidance on configuring billing preferences and creating billing alarms in AWS using CloudWatch. 
    
    -This will help you manage AWS expenses by setting up notifications when billing thresholds are exceeded.

**Prerequisites**

    -AWS Root User Access: Log in with root user credentials to access and modify billing preferences.
    
    -AWS Console Access: Ensure you can navigate to Billing and Cost Management and CloudWatch in the AWS Management Console.
    
**Steps**

1. Accessing Billing and Cost Management
    -Login with the root user credentials.
    -Click on the Profile Name in the AWS Console, then select Billing and Cost Management from the dropdown.
    -The billing section will automatically be in global view, so no specific region selection is required.
3. Configuring Billing Preferences
    -In the left-hand navigation menu, scroll down to Billing Preferences.
    -Find the Invoice Delivery Preferences section and click Edit.
    -Check the box to enable invoice delivery, then click Update.
    -In the Alert Preferences section (on the right), click Edit.
    -Check the alert notification checkbox, then enter your preferred email address in the designated field.
    -Click Update to save your preferences.
4. Setting Up a Billing Alarm in CloudWatch
    -Search for CloudWatch in the AWS Console search bar and select it from the results.
    -In the CloudWatch dashboard, select All Alarms in the left-hand menu.
    -Create Alarm: Click on the Create Alarm button in the center of the page (avoid using the right-side button, as it is for global alarms).
5. Defining Alarm Metrics
    -In the metrics section, click Select Metric.
    -Ensure your region is set to N. Virginia (us-east-1).
    -Under Billing, select Total Estimated Charges and check the box beside the USD currency option.
    -Click Select Metric.
6. Setting Alarm Conditions
    -Set the condition to Greater Than or Equal To and enter a threshold value (e.g., $2 or $5).
    -Click Next.
7. Configuring Notifications
    -In the notification section, select In Alarm and choose Create a Topic.
    -Keep the default topic name, then enter your Email ID in the Email Endpoint field.
    -Click Create Topic and scroll down to click Next.
8. Finalizing Alarm Setup
    -Enter a descriptive name for the alarm in the Alarm Name field.
    -Click Next to review your settings, then select Create Alarm. The billing alarm is now active.
9. Confirming Email Subscription
    -Check your email inbox for a subscription confirmation email from AWS.
    -Click the Confirm Subscription link in the email to activate notifications for your billing alarm.**
