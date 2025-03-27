# Cloud-Watch

AWS CloudWatch Alarm with SNS for High CPU Usage Monitoring
I set up a CloudWatch alarm to monitor CPU utilization and receive email notifications using SNS when the threshold exceeds 50%.

Step 1: Create an SNS Topic
Navigated to AWS SNS Console → Topics → Create Topic
Gave the topic a name (HighCPUAlert) and selected Standard type
Clicked Create Topic

Step 2: Subscribe to the SNS Topic
Opened AWS SNS Console → Subscriptions → Create Subscription
Selected the HighCPUAlert topic
Chose Email as the protocol
Entered my email address and clicked Create Subscription
Verified the email by clicking on the confirmation link received in my inbox

Step 3: Create a CloudWatch Alarm for CPU Utilization
Navigated to CloudWatch Console → Alarms → Create Alarm
Clicked Select Metric → EC2 Metrics
Selected Per-Instance Metrics and filtered using my EC2 instance ID
Chose CPU Utilization and clicked Select Metric

Set the conditions:
Threshold type: Static
Whenever CPU Utilization is Greater than 50%
Period: 5 minutes
Under Actions, added the SNS topic HighCPUAlert to receive alerts
Clicked Create Alarm

Step 4: Testing the Alarm by Increasing CPU Usage
To trigger the CloudWatch alarm, I increased CPU utilization beyond 50% on my Amazon Linux instance.

Commands to Stress Test the CPU on Amazon Linux
Install stress-ng package
sudo dnf install -y stress-ng

Run CPU stress test for 5 minutes
stress-ng --cpu 4 --timeout 300

Stop the stress test manually if needed
pkill stress-ng

After running the stress test, I monitored the CloudWatch metrics. Once CPU usage crossed 50%, I received an SNS email notification confirming that the alarm was triggered.
