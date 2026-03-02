🚀 Host a Static Website on AWS EC2 using Apache
📌 Project Overview

This project demonstrates how to deploy a static website on an EC2 instance using Apache Web Server.

It includes:

EC2 instance creation

Security group configuration

Apache installation

Website deployment

Public access via IP

🛠 Technologies Used

AWS EC2

Amazon Linux 2

Apache (httpd)

SSH

SCP

📋 Prerequisites

AWS account

Key pair (.pem file)

Security group rules:

SSH (22) → My IP

HTTP (80) → 0.0.0.0/0


🧪 Step 1: Launch EC2 Instance

Go to AWS Console → EC2 → Launch Instance

Select Amazon Linux 2

Choose instance type: t2.micro

Attach security group allowing SSH and HTTP

Launch instance and copy Public IP


🔐 Step 2: Connect to EC2
ssh -i "mum-key.pem" ec2-user@<PUBLIC-IP>


🌐 Step 3: Install Apache


sudo yum update -y

sudo yum install httpd -y

sudo systemctl start httpd

sudo systemctl enable httpd

sudo systemctl status httpd

📂 Step 4: Upload Website File

From local machine:

scp -i "mum-key.pem" website.zip ec2-user@<PUBLIC-IP>:/home/ec2-user/


📦 Step 5: Extract Website
sudo yum install unzip -y
unzip website.zip


📁 Step 6: Move Files to Web Root

Apache serves files from:

/var/www/html


Move website files:

sudo cp -r folder-name/* /var/www/html/


🔒 Step 7: Set Permissions
sudo chown -R apache:apache /var/www/html
sudo chmod -R 755 /var/www/html


🌍 Step 8: Access Website

Open browser and visit:

http://<PUBLIC-IP>


Website should load successfully.

✅ Result

Successfully deployed a static website on AWS EC2 using Apache Web Server.

That’s it. Clean. Professional. Interview-ready.

If you want, I can now show you how to make this README look more advanced — like adding architecture explanation or adding screenshots section.
