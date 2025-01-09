# NBA QuickNotify

NBA QuickNotify is a notification system that provides real-time NBA game day alerts. This project leverages AWS services such as SNS, IAM, Lambda, and EventBridge to deliver timely notifications via email. It’s an easy-to-set-up solution for staying updated on the latest NBA game events.

---

## Features

- **Real-Time Notifications**: Receive game day alerts directly via email.
- **Customizable Schedule**: Set your preferred frequency for updates.
- **AWS Integration**: Uses scalable and reliable AWS services.

---

## Project Structure

```
NBA-QuickNotify/
|
|-- src/
|   |-- gd_notifications.py   # Lambda function code for notifications
|
|-- .gitignore               # Git ignore file for untracked files
|-- README.md                # Documentation file
|-- LICENSE                  # License file
```

---

## Prerequisites

Before starting, ensure you have the following:

1. An **AWS Account**.
2. An **NBA API Key** (Sign up with an NBA stats provider like SportsData.io).

---

## Step-by-Step Setup

### **Step 1: Amazon SNS (Simple Notification Service)**

1. Log into your AWS Management Console.
2. Search for **Amazon SNS** in the search bar.
3. Create a **Topic** (e.g., `DemoTopic`).
4. Create a **Subscription**:
   - Protocol: **Email**
   - Endpoint: Enter your email address.
5. Confirm the subscription via the confirmation email sent to your inbox.

---

### **Step 2: IAM (Identity and Access Management)**

1. Navigate to the **IAM** service in the AWS Management Console.
2. Create a **Policy** that grants permissions to use the SNS topic and Lambda.
3. Create a **Role**:
   - Attach the policy you created.
   - Also attach the **AWSLambdaBasicExecutionRole** policy.

---

### **Step 3: AWS Lambda**

1. Create a **Lambda Function** (e.g., `Demo_notification`).
2. Change the execution role to the one created in Step 2.
3. Under the **Function Code** section:
   - Copy the content of the `src/demo_notifications.py` file from the repository.
   - Paste it into the inline code editor.
4. Add the following **Environment Variables**:
   - `NBA_API_KEY`: Your NBA API key.
   - `SNS_TOPIC_ARN`: The ARN of the SNS topic created earlier.
5. Update the **timeout setting** in the general configuration (recommended: 1–3 minutes).
6. Deploy the function.

If configured correctly, you should receive a test email after execution.

---

### **Step 4: Amazon EventBridge**

1. Open the **EventBridge** service in the AWS Management Console.
2. Create a **Rule**:
   - Event Source: **Schedule**.
   - Define the schedule using a cron expression (e.g., hourly updates).
3. Under **Targets**, select the Lambda function created earlier (`Demo_notification`).
4. Save the rule.

---

## Testing the System

1. Open the **Lambda Function** in the AWS Management Console.
2. Create a **Test Event** to simulate execution.
3. Check **CloudWatch Logs** for errors or successful execution logs.
4. Verify that email notifications are delivered to the subscribed addresses.

---

## Future Enhancements

- Add support for SMS notifications.
- Extend functionality to include notifications for other sports.
- Enhance error handling and logging.

---

## Technologies Used

- **AWS SNS**: For notifications.
- **AWS Lambda**: For running the notification logic.
- **AWS EventBridge**: For scheduling notifications.
- **Python**: For processing data and integrating with the NBA API.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

