
---

# Bash Automated Backup System

Automated backup solution using Bash scripts with optional upload to **AWS S3**. Supports scheduling with `cron` and logging.

---

## Features

* Take compressed backups (`.tar.gz`) of specified directories.
* Automatic timestamped filenames for easy versioning.
* Logging of backup operations.
* Optional upload to **AWS S3**.
* Fully automated via `cron` scheduling.
* Error handling for duplicate files and missing dependencies.

---

## Requirements

* Linux environment
* Bash shell
* AWS CLI (for S3 integration)
* Access to an AWS account with proper IAM permissions

---

## Setup & Usage

### 1. Backup Script (Local)

```bash
#!/bin/bash
time=$(date +%m-%d-%y_%H_%M_%S)
Backup_file=$1
Dest=/home/ubuntu/backup
filename=file-backup-$time.tar.gz
LOG_FILE="/home/ubuntu/backup/logfile.log"

if [ -z "$Backup_file" ]; then
    echo "Please, Enter the directory that you want to backup" | tee -a "$LOG_FILE"
    exit 2
fi

if [ -f $filename ]; then
    echo "Error file $filename already exists!" | tee -a "$LOG_FILE"
else
    tar -czvf "$Dest/$filename" "$Backup_file"
    echo "Backup completed successfully. Backup file: $Dest/$filename" | tee -a "$LOG_FILE"
fi
```

Run the script:

```bash
bash backup-script.sh /path/to/directory
```

---

### 2. Backup Script with AWS S3 Upload

```bash
#!/bin/bash
time=$(date +%m-%d-%y_%H_%M_%S)
Backup_file=/home/ubuntu/bash
Dest=/home/ubuntu/backup
filename=file-backup-$time.tar.gz
LOG_FILE="$Dest/logfile.log"
S3_BUCKET="s3-new-bash-course"
FILE_TO_UPLOAD="$Dest/$filename"

if ! command -v aws &> /dev/null; then
  echo "AWS CLI is not installed. Please install it first."
  exit 2
fi

if [ -f $filename ]; then
    echo "Error file $filename already exist!" | tee -a "$LOG_FILE"
else
    tar -czvf "$Dest/$filename" "$Backup_file"
    echo "Backup completed successfully. Backup file: $Dest/$filename" | tee -a "$LOG_FILE"
    aws s3 cp "$FILE_TO_UPLOAD" "s3://$S3_BUCKET/"
fi
```

---

### 3. Automate with Cron

Edit the cron file:

```bash
sudo vim /etc/crontab
```

Add schedule (example: every 2 minutes):

```
*/2 * * * * root /home/ubuntu/backup-script.sh
```

---

### 4. AWS Setup

1. Create IAM user and role with permissions:

   * `AmazonS3FullAccess`
   * `AmazonSSMFullAccess`
2. Attach IAM role to your EC2 instance.
3. Configure AWS CLI:

```bash
aws configure
```

4. Create S3 bucket:

```bash
aws s3api create-bucket --bucket s3-new-bash-course --region us-east-1
```

---

### 5. Logging

* All operations are logged to: `/home/ubuntu/backup/logfile.log`
* Includes errors and backup completion messages.

---

### 6. Clean Up S3 Bucket

```bash
aws s3 rb s3://s3-new-bash-course --force
```

---

### Author

ahmed mostafa

---


تمام 💪، ده وصف قصير واحترافي تقدر تحطه في الـ CV للمشروع:

---

**Bash Automated Backup System**

* Developed a fully automated backup solution using Bash scripts for Linux servers.
* Implemented timestamped backups, logging, and error handling for reliability.
* Integrated with **AWS S3** to upload backups, ensuring offsite storage and disaster recovery.
* Scheduled automated execution using `cron` to run backups periodically without manual intervention.
* Demonstrated skills in **Bash scripting, AWS CLI, Linux system administration, and automation**.

---

لو تحب، أقدر أصيغ نسخة أقصر جدًا مناسبة لقسم **Projects** في CV بحيث تاخد سطر أو سطرين بس 👌

تحب أعملها؟


تمام 😎، ده نسخة قصيرة جدًا مناسبة لقسم **Projects** في CV:

---

**Bash Automated Backup System** – Automated Linux backups using Bash scripts with logging, cron scheduling, and AWS S3 integration for offsite storage.

---

لو تحب، أقدر أصيغ لك كمان **نسخة ثانية بصياغة أكثر “Impact”** تبرز مهاراتك كـ DevOps Engineer وتخليها ملفتة لأصحاب العمل. تحب أعملها؟

