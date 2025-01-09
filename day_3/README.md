# NBA Data Lake Project

## Overview
This project sets up a data lake for NBA sports analytics using AWS services (S3, Glue, Athena) and data from Sportsdata.io. The setup involves creating an S3 bucket, fetching NBA player data via an API, uploading the data to S3, and configuring AWS Glue and Athena for analytics.

## Prerequisites
1. **Sportsdata.io Account:**
   - Sign up on [Sportsdata.io](https://sportsdata.io) and start a free trial for the NBA API.
   - Confirm your account via email and access the Developer Portal.
   - Navigate to the NBA section under "Standings," locate "Query String Parameters," and copy your API key.
 
2. **Development Environment:**
   - Install [Visual Studio Code (VSCode)](https://code.visualstudio.com/).
   - Install the Python extension for VSCode.
   - Ensure Python is installed on your system. Verify using:
     ```bash
     python --version
     ```

3. **AWS Account:**
   - Log in to your AWS account.
   - Familiarize yourself with the AWS Management Console.

## Setup Instructions

### 1. Environment Setup
1. Open a terminal or command prompt.
2. Create a virtual environment:
   ```bash
   python -m venv venv
   ```
3. Activate the virtual environment:
   - Windows:
     ```bash
     venv\Scripts\activate
     ```
   - Mac/Linux:
     ```bash
     source venv/bin/activate
     ```
4. Install the required Python libraries:
   ```bash
   pip install boto3 python-dotenv requests
   ```

### 2. AWS CloudShell Setup
1. Log in to your AWS account.
2. Click on the **CloudShell** button at the top of the console.
3. In the CloudShell CLI, create a Python script file:
   ```bash
   nano setup_nba_data_lake.py
   ```
4. Copy and paste the provided project code into `setup_nba_data_lake.py`.

### 3. Update the Code
1. Locate the following lines in the code:
   ```python
   SPORTS_DATA_API_KEY=your_sportsdata_api_key
   NBA_ENDPOINT=https://api.sportsdata.io/v3/nba/scores/json/Players
   ```
2. Replace `your_sportsdata_api_key` with your actual Sportsdata.io API key.
3. Update the bucket name in the code to a unique name, e.g.,
   ```python
   bucket_name = "my-unique-sports-data-lake"
   ```

4. Save the file and exit:
   ```bash
   Ctrl+O (save) and Ctrl+X (exit)
   ```

### 4. Run the Script
1. Execute the script in CloudShell:
   ```bash
   python3 setup_nba_data_lake.py
   ```

### 5. Verify Resources
#### S3 Bucket:
1. In the AWS Management Console, search for **S3** in the search bar.
2. Open the S3 service and locate your bucket (e.g., `my-unique-sports-data-lake`).
3. Navigate to the `raw-data` folder in your bucket and verify the presence of the `nba_player_data.json` file.
4. Open the file to view the fetched NBA data.

#### Glue and Athena:
1. Check AWS Glue for the created database and table.
2. In Athena, verify the output location and run queries on the `nba_players` table.

## Notes
- Ensure your API key is valid and you are using the correct endpoint.
- AWS services may incur costs; monitor your usage.
- The bucket name must be globally unique.

## Troubleshooting
- **Invalid Bucket Name:** Ensure your bucket name contains only lowercase letters, numbers, and hyphens.
- **No Data in S3:** Confirm the API key and endpoint in the script.
- **Errors in Glue or Athena:** Check the permissions of your AWS IAM user.

## Additional Information
For detailed documentation, visit the official AWS and Sportsdata.io documentation:
- [AWS S3](https://docs.aws.amazon.com/s3/)
- [AWS Glue](https://docs.aws.amazon.com/glue/)
- [AWS Athena](https://docs.aws.amazon.com/athena/)
- [Sportsdata.io API Documentation](https://sportsdata.io/developers)

---

**Author:** [Your Name]  
**Date:** January 2025  
**Purpose:** Build a scalable data lake for NBA analytics.

