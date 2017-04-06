footer: © NodeProgram.com, Node.University and Azat Mardan 2017
slidenumbers: true
theme: Merriweather, 8
build-lists: true


# AWS Intro
##

![inline 100%](images/azat.jpeg)
Azat Mardan @azat_co

![inline right](images/nu.png)

---

# Module 1: Cloud and AWS Basics

---

## Why cloud?

Yell out loud the benefits! 🔊

---

# Overview of cloud computing

* IaaS
* PaaS
* FaaS
* SaaS

---

# Main concepts: Regions and AZs

---

# Main AWS Services

* EC2
* S3
* Glacier
* EBS
* VPC
* CloudWatch
* Alerts
* RDS

---

# Billing and calculator

---

# What you need or lab 0

---

## Slides&code

Repo: <https://github.com/azat-co/aws-intro>

Git clone (you can fork first too):

```
git clone https://github.com/azat-co/aws-intro.git
```

Download with CURL and unzip (create a new folder):

```
curl  https://codeload.github.com/azat-co/aws-intro/zip/master | tar -xv
```

---

## AWS account: Free tier

* Sign up for free tier with an email you have access to
* Random verification (phone call or wait - ask me for access to my account)
* Debit/credit Card for verification and paid services



---

## AWS account: Free tier (cont)

Free tier: <https://aws.amazon.com/free>, examples:

* EC2: 750 hours of t2.micro (~1 month of 1 EC2) - more than enough for this class and then some more
* S3: 5Gb
* RDS: 750 hours
* Lambda: 1,000,000 requests/mo
* More products!

---

## Node and npm

```
node --version
npm --version
```

I develop natively on my dev machine, but you can use another EC2 instance

---

# Questions?

---

## Checklist

* Slides, labs and code  <https://github.com/azat-co/aws-intro>
* AWS account
* Node and npm

15 minutes to download and install

---

# ❓ Questions? ❓

---

# Module 2: Main EC2 Concepts

---

# EC2 Lifecycle

![inline](images/instance_lifecycle.png)


---

# "Stopped" to "running"

* Rounded to an hour for billing (no charges for "stopped")
* A new private IPv4 address unless in VPC or IPv6
* A new public IPv4
* Only EBS instances (more on storage later)
* More [*Differences Between Reboot, Stop, and Terminate*](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2-instance-lifecycle.html)

---

# Images

![inline](images/architecture_ami_instance.png)

---

# Images

* AMI can convert to/from other image types
* Marketplace
* Can create your own images
* images IDs for the same OS differ from region to region
* AMIs can be backed by EBS or instance store

---

# Images (cont)

* OS, e.g., Amazon Linux
* HVM
* bit, e.g., 64 bit
* Any software?

---

# Root Device: EBS vs. Instance store

* EBS is faster to boot
* More EBS can be added later
* EBS allows to stop and restart
* Persistent —EBS data is saved
* Comparison [Storage for the Root Device](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ComponentsAMIs.html#storage-for-the-root-device)


---

# Types

* Category (t)
* Generation (2)
* Size (micro)

t2.micro

All types: <https://aws.amazon.com/ec2/instance-types>

---

# IAM

---

# User Data

---

# Storage

* SSD
* Provisioned
* Magnetic

---

# Tags

---

# Spot vs. Reserved

---

# Key pairs

---

# Security groups

---

# ELB

# Elastic IP

---

# VPC, subnets and AZs

^We will talk more about VPC and subnets in the next modules

---

![inline](images/aws_regions.png)

---

![inline](images/EC2_select_region.png)

---

|Code|Name|
|--- |--- |
|us-east-1|US East (N. Virginia)|
|us-east-2|US East (Ohio)|
|**us-west-1**|**US West (N. California)** 👈 *USE THIS FOR LABS*|
|us-west-2|US West (Oregon)|
|ca-central-1|Canada (Central)|
|eu-west-1|EU (Ireland)|
|eu-central-1|EU (Frankfurt)|
|eu-west-2|EU (London)|
|ap-northeast-1|Asia Pacific (Tokyo)|
|ap-northeast-2|Asia Pacific (Seoul)|
|ap-southeast-1|Asia Pacific (Singapore)|
|ap-southeast-2|Asia Pacific (Sydney)|
|ap-south-1|Asia Pacific (Mumbai)|
|sa-east-1|South America (São Paulo)|

---

# Stop vs terminate

---

# ❓ Questions? ❓

---

# Demo Time 💻

* Demo: Launching EC2
  * Launching EC2: images (Amazon Linux), types (t2.micro), storage (8Gb), tags (role=aws-course)
  * Creating security groups (ICMP for ping, SSH and HTTP are open)
  * Working with SSH key pairs
  * Connecting to EC2 via SSH

---

# ❓ Questions? ❓

---

# Lab 1: WP is King

Task: Create an instance with WordPress, make the website visible in the browser *publicly*

Detailed instruction in labs/lab-01.md

10 min

---

# Module 3: Environment and App Deploy Automation

---

## SSH-ing into each new machine manually is not optimal... what to do?

---

## User Data

2nd step, advanced settings

---

![fit](images/user-data-ec2-config.png)

---

When you specify user data, note the following:

* User data is treated as opaque data (AWS won't check it, it's up to instance to interpret and execute)
* Executed only at launch
* Limited to 16 KB. (raw data, not base64-encoded)
* User data must be base64-encoded before being submitted to the API. The AWS CLI and the Amazon EC2 web console do encoding for you.  For more information about base64 encoding, see <http://tools.ietf.org/html/rfc4648>.
* Must start with `#!/bin/bash` or similar for shell

---

Note: There are many other solutions for environment and app built, test and deploy automation. We will cover some of them in *AWS Intermediate*.

---

## Demo: User Data for Apache httpd and HTML page

```bash
#!/bin/bash
yum install -y httpd
service httpd start
echo "Hello World!" > /var/www/index.html
```

---

## Demo: User Data for Apache httpd, PHP and PHP code

```bash
#!/bin/bash
yum update -y
yum install -y httpd24 php56 mysql55-server php56-mysqlnd
service httpd start
chkconfig httpd on
groupadd www
usermod -a -G www ec2-user
chown -R root:www /var/www
chmod 2775 /var/www
find /var/www -type d -exec chmod 2775 {} +
find /var/www -type f -exec chmod 0664 {} +
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
echo "<?php echo 'Hello World!' ?>" > /var/www/html/index.php
```

---

## Testing Apache httpd, PHP and Hello World

<http://PUBLIC_URL/> or <http://PUBLIC_URL/index.php>
<http://PUBLIC_URL/phpinfo.php>

Note: Never leave phpinfo in production because attackers can use the system info against the system!

---


## Cloud Init

Same Apache httpd, PHP and phpinfo config in User Data but with cloud-init instead of bash:

```
#cloud-config
repo_update: true
repo_upgrade: all

packages:
 - httpd24
 - php56
 - mysql55-server
 - php56-mysqlnd
```

---

## Cloud Init (cont)

Same Apache httpd, PHP and phpinfo config in User Data but with cloud-init instead of bash:


```
runcmd:
 - service httpd start
 - chkconfig httpd on
 - groupadd www
 - [ sh, -c, "usermod -a -G www ec2-user" ]
 - [ sh, -c, "chown -R root:www /var/www" ]
 - chmod 2775 /var/www
 - [ find, /var/www, -type, d, -exec, chmod, 2775, {}, + ]
 - [ find, /var/www, -type, f, -exec, chmod, 0664, {}, + ]
 - [ sh, -c, 'echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php' ]
```

---

# Cloud Init (cont)

For trouble shooting, cloud init logs are in `/var/log/cloud-init-output.log`.

More docs: http://cloudinit.readthedocs.io/en/latest/index.html

---

## Demo: User Data for a Node app with pm2 (restart on reboot)

hello-world-server.js:

```js
const port = 3000
require('http')
  .createServer((req, res) => {
    console.log('url:', req.url)
    res.end('hello world')
  })
  .listen(port, (error)=>{
    console.log(`server is running on ${port}`)
  })
```


---

# User Data Bash for Node app with pm2 (Amazon Linux Example)

---

```bash
#!/bin/bash -ex
exec > >(tee /var/log/user-data.log|logger -t user-data -s 2>/dev/console) 2>&1
curl --silent --location https://rpm.nodesource.com/setup_6.x | bash -
yum -y install nodejs
npm i -g pm2@2.4.3
echo "const port = 3000
require('http')
  .createServer((req, res) => {
    console.log('url:', req.url)
    res.end('hello world')
  })
  .listen(port, (error)=>{
    console.log(`server is running on ${port}`)
  })
" >> /home/ec2-user/hello-world-server.js
crontab -l | { cat; echo "@reboot pm2 start /home/ec2-user/hello-world-server.js -i 0 --name \"node-app\""; } | crontab -
sudo reboot
```

---

rc.d: (works but has two versions of pm2 - one in /etc/.pm2 and another in ec2-user)

```bash
#!/bin/bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash
. /.nvm/nvm.sh
sudo sed -i '$i export NVM_DIR="$HOME/.nvm"' /home/ec2-user/.bashrc
sudo sed -i '$i [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm' /home/ec2-user/.bashrc
nvm install 6.7
echo "const port = 3000
require('http')
  .createServer((req, res) => {
    console.log('url:', req.url)
    res.end('hello world')
  })
  .listen(port, (error)=>{
    console.log(`server is running on ${port}`)
  })
" >> /home/ec2-user/hello-world-server.js
npm i -g pm2@2.4.3
sudo sed -i '$i export PATH=$PATH:/.nvm/versions/node/v6.7.0/bin' /home/ec2-user/.bashrc
sudo sed -i '$i . /.nvm/nvm.sh' /etc/rc.d/rc.local
sudo sed -i '$i pm2 start /home/ec2-user/hello-world-server.js -i 0 --name \"node-app\"' /etc/rc.d/rc.local
sudo reboot
```

```
#!/bin/bash
. /.nvm/nvm.sh
pm2 start /home/ec2-user/hello-world-server.js -i 0 --name "node-app"
```

sudo adduser node
sudo su - ec2-user

```bash
#!/bin/bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash
. /.nvm/nvm.sh
sudo sed -i '$i export NVM_DIR="$HOME/.nvm"' /home/ec2-user/.bashrc
sudo sed -i '$i [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm' /home/ec2-user/.bashrc
nvm install 6.7
echo "const port = 3000
require('http')
  .createServer((req, res) => {
    console.log('url:', req.url)
    res.end('hello world')
  })
  .listen(port, (error)=>{
    console.log(`server is running on ${port}`)
  })
" >> /home/ec2-user/hello-world-server.js
npm i -g pm2@2.4.3
#pm2 start /home/ec2-user/hello-world-server.js
#pm2 save
#pm2 startup
sudo sed -i '$i export PATH=$PATH:/.nvm/versions/node/v6.7.0/bin' /home/ec2-user/.bashrc
sudo sed -i '$i . /.nvm/nvm.sh' /etc/rc.d/rc.local
sudo sed -i '$i pm2 start /home/ec2-user/hello-world-server.js -i 0 --name \"node-app\"' /etc/rc.d/rc.local
sudo reboot

sudo env PATH=$PATH:/.nvm/versions/node/v6.7.0/bin /.nvm/versions/node/v6.7.0/lib/node_modules/pm2/bin/pm2 startup systemv -u ec2-user --hp /home/ec2-user
sudo reboot
```

---

## Pulling code from S3 (Amazon Linux Example)


```bash
#!/bin/bash
yum install -y aws-cli
cd /home/ec2-user/
aws s3 cp 's3://{my-private-bucket}/{app-folder}/lastest.zip' /var/app \
  --region {bucket_region} # requires IAM role to access S3
# unzip and launch
```

Note: *AWS CLI covered in the AWS Intermediate course*

---

## Pulling code from private GitHub repository (Amazon Linux Example)

```bash
#!/bin/bash
yum install -y git-all
git clone https://username:password@github.com/{username}/{private_repository}.git
```

Note: *You can also use SSH (private key on EC2 and public on GitHub)*

---

# ❓ Questions? ❓

----

## Lab 2: Hello world Baby

Task: Launch an instance with "Hello World" HTTP server (Node.js), make the website visible in the browser *publicly*. Do not SSH!

Detailed instructions in labs/lab-02.md, Node server code is in code/index.js

Time:20 min


---

# ❓ Questions? ❓

## Module 4: Auto Scaling

* Alerts and CloudWatch
* Demo: Create a launch config, auto scaling group and policy to increase instances
* Demo: Create a launch configuration, autoscaling group and see if it works
* Lab 3: Deploy 2 Node apps under ELB, load test it to see if autoscaling works


---
