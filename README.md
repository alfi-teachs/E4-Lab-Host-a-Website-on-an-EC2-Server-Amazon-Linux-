# E4-Lab-Host-a-Website-on-an-EC2-Server-Amazon-Linux-
Objective  Launch an EC2 instance and host a static website using Apache HTTP Server.

Step 1: Launch EC2 Instance

Go to AWS Console → EC2 → Launch Instance

Choose:

AMI: Amazon Linux 2

Instance Type: t2.micro (Free tier)

Create or select a key pair.

Create or select a Security Group and add:

Type	Port	Source
SSH	22	My IP
HTTP	80	0.0.0.0/0

⚠ HTTP rule is required to access the website in the browser.

Launch the instance.

Copy the Public IP address.

Step 2: Connect to EC2 (SSH)

From your local machine:

ssh -i "C:\Users\almal\Downloads\mum-key.pem" ec2-user@52.66.253.200


(Replace with your actual key path and public IP.)

Step 3: Install and Start Apache

Check if Apache is installed:

sudo systemctl status httpd


If not installed:

sudo yum install httpd -y


Start Apache:

sudo systemctl start httpd


Enable Apache to start on boot:

sudo systemctl enable httpd


Verify Apache is running:

sudo systemctl status httpd

Step 4: Upload Website Files to EC2

Exit from EC2:

exit


From your laptop, copy the zip file:

scp -i "C:\Users\almal\Downloads\mum-key.pem" "C:\Users\almal\Downloads\yourfile.zip" ec2-user@52.66.253.200:/home/ec2-user/

Step 5: Extract Website Files

Reconnect to EC2:

ssh -i "C:\Users\almal\Downloads\mum-key.pem" ec2-user@52.66.253.200


Install unzip (if needed):

sudo yum install unzip -y


Unzip the file:

unzip yourfile.zip


Check extracted folder:

ls

Step 6: Move Files to Apache Web Directory

Apache serves files from:

/var/www/html


Move website files:

sudo cp -r folder-name/* /var/www/html/


Verify:

ls /var/www/html

Step 7: Set Proper Permissions

Instead of using 777 (not recommended), use:

sudo chown -R apache:apache /var/www/html
sudo chmod -R 755 /var/www/html


This is safer and correct for production environments.

Step 8: Access Website in Browser

Open browser and enter:

http://52.66.253.200


(Replace with your EC2 Public IP.)

If everything is correct, your website will load.

🔎 Troubleshooting

If site is not opening:

Check Security Group → HTTP port 80 must allow 0.0.0.0/0

Check Apache status:

sudo systemctl status httpd


Check if instance has a Public IP

Make sure Internet Gateway is attached to the VPC (if using custom VPC)

Result

Successfully hosted a static website on an EC2 instance using Apache HTTP Server.

