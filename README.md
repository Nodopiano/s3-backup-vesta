# s3-backup-vesta 

One-line script that takes daily backup weekly and uploads it to S3. 
We create a role and user with minimum allowed actions(only one) and we manage backups Lifecycle on AWS side.

## Amazon AWS

1. Go to https://console.aws.amazon.com/iam/home#policies 
Click "Create Policy" - > Select "Policy Generator" -> Choose Amazon s3, one action "s3:PutObject" and 
       "Resource": arn:aws:s3:::some.yourserver.com/*
2. Go to https://console.aws.amazon.com/iam/home#users create user and attach policy. Also, save Access Key ID and Secret Access Key.
3. Go to https://console.aws.amazon.com/s3/home and create "some.yourserver.com" bucket.
4. Click on the bucket, go to "Properties -> Lifecycle", and "Add Rule". For example, "Permanently Delete 35 Days after the object's creation date".

## Server side

1. Install AWS CLI(http://docs.aws.amazon.com/cli/latest/userguide/installing.html), The simplest way:

  ```
  sudo apt-get install python-pip -y
  sudo pip install awscli
  ```
  
2. Configure AWS cli
  
  ``` 
  root@some:~# aws configure
  AWS Access Key ID [None]: AKIAJJDXXXXXXXXXXXX
  AWS Secret Access Key [None]: ushi6XXXXXXXXXXXXZJqstRD1jKi1TjVxGbPW
  Default region name [None]: us-east-1
  Default output format [None]: json
  ```

## Weekly Cron

Create or wget s3-backup-vesta script to /etc/cron.weekly folder.

```
wget -O /etc/cron.weekly/s3-backup-vesta https://raw.githubusercontent.com/o1ek/s3-backup-vesta/master/s3-backup-vesta && chmod +x /etc/cron.weekly/s3-backup-vesta
```
