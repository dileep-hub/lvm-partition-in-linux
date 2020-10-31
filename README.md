# lvm-partition-in-linux
https://miro.medium.com/max/875/0*ANVCnSoD77AaV3Xs.jpg
![code](https://miro.medium.com/max/875/0*ANVCnSoD77AaV3Xs.jpg)<br> <br>
🔰 Creating High Availability Architecture with AWS CLI 🔰



Image for post
In this article we gonna integrate AWS instance, EBS, S3 (STORAGE), Cloud Front all together and configure the Web server
✅ Here we launched a new instance upon AWS.
Image for post
CODE: aws ec2 run-instances — image-id ami-0e306788ff2473ccb — instance-type t2.micro — count 1 — subnet-id subnet-e5676e8d — security-group-ids sg-02dd8e7bfe5ad94e0 — key-name awsclass2020key
Image for post
Info of our instance
Check in aws also → instance launched (aws-cli-arth)
Image for post
instance lauched
✅ [Now lets configure the webserver on our instance. For that lets install httpd in our instance
Image for post
Command: yum install httpd
Now lets check the status of httpd
Image for post
cmd: systemctl status httpd
As it is inactive lets start the httpd
Image for post
now it is active
Finally we have configured apache webserver in our instance
✅ Now lets create EBS volume
Image for post
command: aws ec2 create-volume — availability-zone ap-south-1a — size 1
Image for post
This is our instance storage /dev/xvda → is our root storage
Attach the EBS volume to the instance
Image for post
COMMAND: aws ec2 attach-volume — volume-id vol-0263566aa0ce0f421 — instance-id i-0fc29c030cd1b9465 — device /dev/sdf
Now check in AWS console
Image for post
Image for post
Here u can see EBS volume has been attached
✅ Now lets create Partition for the new attached volume
Here # fdisk /dev/xvdf → to go inside it and ‘ n’ to create new partition and ‘p’ to make a primary partition .Finally ‘w’ to save it
Image for post
✅ Now format it
Image for post
Formatted ext4 is a one type of inode table
Now lets mount the device to the /var/www/html → becoz to make it availble for the webserver → root document (/var/www/html) for webserver
Image for post
✅ Now create a web page in the /var/www/html folder
Image for post
✅ Now lets create S3 bucket to save the static files.
Image for post
command: aws s3api create-bucket — bucket dileep142 — region ap-south-1 — create-bucket-configuration LocationConstraint=ap-south-1
You can check in aws GUI it is created.
Image for post
Now u can upload any of ur pic in the bucket so that it will be visible in the website.
Image for post
copy the url provided by the S3 and make it public
Now paste this url in ur HTML file created in the /var/www/html
Image for post
Now finally lets create cloudfront distribution.
Which helps our website to be very fast and make user satisfaction.
Image for post
created distribution
Image for post
✅Now we can check weather our instance configured with webserver or not by searching http://<ip>/<html file name>
Image for post
By the help cloudfront our website will be very fast (low latency) and will be available for anyone in the world with the same speed(velocity)
@HIGH AVAILABILITY ARCHITECTURE
⏩ By this we finally done the Task-6
THANK YOU
