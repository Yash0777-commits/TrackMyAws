# Track-My-Aws

TrackMyAws is a Bash script designed to automate the process of listing resources in an AWS account for specific services and regions. The script logs the details into timestamped files for easy tracking and management.

---

## Features

- Lists AWS resources for services such as EC2, S3, RDS, VPC, IAM, Lambda, and more.
- Supports specifying AWS region and service as input parameters.
- Stores the output in a timestamped log file.
- Designed for daily execution via cron jobs.

---

## Prerequisites

### 1. Install AWS CLI
Ensure the AWS CLI is installed on your system. You can install it using the following command:

```bash
sudo apt install awscli -y  # For Ubuntu/Debian
sudo yum install aws-cli -y # For CentOS/Red Hat
```

### 2. Configure AWS CLI
Configure the AWS CLI with your credentials:

```bash
aws configure
```
You will be prompted to enter:
- AWS Access Key ID
- AWS Secret Access Key
- Default region
- Default output format

### 3. Set Up Required Permissions
Ensure that the IAM user or role you are using has sufficient permissions to list resources for the services you want to monitor.

### 4. Install Cron (if not already installed)

```bash
sudo apt install cron -y  # For Ubuntu/Debian
sudo yum install cronie -y # For CentOS/Red Hat
```

Ensure the cron service is running:
```bash
sudo systemctl start cron
sudo systemctl enable cron
```

---

## Installation

### 1. Clone the Repository
Clone the repository containing the `TrackMyAws` script:

```bash
git clone <repository-url>
cd <repository-folder>
```

### 2. Set Execute Permissions
Make the script executable:

```bash
chmod +x TrackMyAws.sh
```

### 3. Verify Script Functionality
Test the script with sample inputs:

```bash
./TrackMyAws.sh us-east-1 ec2
```

This will log the details of EC2 instances in the `us-east-1` region.

---

## Usage

### Syntax
```bash
./TrackMyAws.sh <aws_region> <aws_service>
```

### Examples
- List EC2 instances in the `us-east-1` region:
  ```bash
  ./TrackMyAws.sh us-east-1 ec2
  ```
- List S3 buckets:
  ```bash
  ./TrackMyAws.sh us-east-1 s3
  ```

The output will be saved in the `logs` directory with a filename like `aws_resources_<date>.log`.

---

## Automate with Cron

To execute the script automatically every day:

### 1. Edit Cron Tab
Open the cron editor:

```bash
crontab -e
```

### 2. Add Cron Job
Add the following line to schedule the script to run daily at midnight:

```bash
0 0 * * * /path/to/TrackMyAws.sh <aws_region> <aws_service> >> /path/to/cron.log 2>&1
```

Replace:
- `/path/to/TrackMyAws.sh` with the full path to the script.
- `<aws_region>` with the desired AWS region (e.g., `us-east-1`).
- `<aws_service>` with the AWS service (e.g., `ec2`).

### 3. Save and Exit
Save the cron file and exit. The script will now run daily.

### 4. Verify Cron Job
Check the list of scheduled cron jobs:

```bash
crontab -l
```

---

## Directory Structure

```plaintext
TrackMyAws/
|-- TrackMyAws.sh       # Main script file
|-- logs/               # Directory for storing log files
```

---

## Troubleshooting

### Logs Not Generated
Ensure that the `logs` directory exists and the script has write permissions:

```bash
mkdir -p logs
chmod +w logs
```

### AWS CLI Errors
Check if the AWS CLI is properly configured:

```bash
aws configure
```

### Debugging Cron Jobs
If the cron job does not execute as expected, check the cron logs:

```bash
sudo tail -f /var/log/syslog  # For Ubuntu/Debian
sudo tail -f /var/log/cron    # For CentOS/Red Hat
```

---

## License
This project is licensed under the MIT License. Feel free to modify and distribute it.

---

## Author
Yash Kumbhar

