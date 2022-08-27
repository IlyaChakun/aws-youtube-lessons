
# Links for download:

1. Git Bash https://git-scm.com/downloads
2. https://winscp.net/eng/download.php

# Example 1

### Script:
1. Create EC2 instance with Linux
   1. Don`t forget to download .pem file to be able to connect to the server
   2. For security group select two rules
      1. For port 22 from anywhere
      2. For port 80 from anywhere
2. SSH on it via git bash and via winscp
   1. ssh -i "your-key.pem" ec2-user@<your-instance-dns>.com
3. Create accessible html page and deploy it via httpd
   1. sudo su 
   2. yum update -y 
   3. yum install -y httpd 
   4. systemctl start httpd  
   5. systemctl enable httpd
   6. echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
4. Test that you receive content
   1. curl localhost:80  (port 80 because it is a default one for httpd)
5. Test via public ip from ec2 instance in your browser


# Example 2

### Script
1. Create EC2 instance with Linux and don`t forget to add userdata
   1. Use [ec2-userdata](./ec2-userdata.sh)
   2. For security group select two rules
      1. For port 22 from anywhere
      2. For port 80 from anywhere
2. Test via public ip from ec2 instance in your browser


# Example 3

### Script
1. Create EC2 instance with Linux
    1. Don`t forget to download .pem file to be able to connect to the server
2. SSH on it via git bash and via winscp
    1. ssh -i "your-key.pem" ec2-user@<your-instance-dns>.com
3. Try to get list of buckets and get error because of creds
   1. aws s3api list-buckets --query "Buckets[].Name" 
4. Go to IAM and create Role with S3FullAccess
5. Attach this role to Ec2
6. Try to get list of buckets again