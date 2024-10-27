Setting Up a Billing Alarm in CloudWatch
Access CloudWatch:

Use the search bar at the top of the AWS Console to search for CloudWatch and select it from the results.
Create a Billing Alarm:

In the CloudWatch dashboard, select All Alarms from the left-hand menu.
Click on the Create Alarm button located in the center of the page (not the right-side "Create Alarm" button, which is for global alarms).
In the Metrics section, click Select Metric.
Ensure that your region is set to N. Virginia (us-east-1).
From the available metrics, select Billing, then choose Total Estimated Charges. Check the box next to the USD currency option and click Select Metric.
Define Alarm Conditions:

Set the threshold condition by choosing Greater Than or Equal To and specify a dollar amount for the alarm threshold (e.g., $2 or $5).
Click Next to proceed.
Configure Notification Options:

In the Notification section, select the In Alarm checkbox, then choose Create a Topic.
Leave the topic name as default, enter your Email ID under the Email Endpoint, and click Create Topic.
Scroll down and select Next to continue.
Finalize the Alarm Setup:

In the Alarm Name field, enter a descriptive name for the alarm, then select Next.
Review the settings and click Create Alarm. Your billing alarm will now be active.
Confirm Email Subscription:

Check your email for a subscription confirmation message from AWS. Click the Confirm Subscription link to activate email notifications for your billing alarm.
