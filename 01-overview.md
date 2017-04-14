footer: © NodeProgram.com, Node.University and Azat Mardan 2017
slidenumbers: true
theme: Merriweather, 8
build-lists: true

# AWS Intro
## Overview

![inline 100%](images/azat.jpeg)
Azat Mardan @azat_co

![inline right](images/nu.png)

---

# Meet Your Instructor

* Name: Azat Mardan
* Author of 14 books and over 12 online courses, taught over 500 engineers in-person and over 25,000 online (Udemy and Node University)
* Works as Capital One Technology Fellow (modeled after IBM and Google Fellows)

---

![fit](images/azats-books-covers.png)

---

# Meet Your Instructor (cont)

* Master of Science in Information Systems Technology from University of Northern Virginia (2007)
* Working on my second Master's degree, this time in Software Engineering and in Harvard University
* Twitter: @azat_co, Online: <http://azat.co>

---

# Why I teach this course?

---

* Gizmo: small startup, used Rackspace
* Storify: small startup, used Joyent and AWS
* DocuSign: didn't use cloud 😞
* Capital One: cloud everywhere

---

# Introduce your self by raising hand ✋

* How many years in technology: 1, 2, 4, 8, or 16?
* Your main language: Java, Python, Ruby, C, JavaScript, or COBOL?
* What are your expectations so that you are 100% satisfied by this course at 5pm?

---

# Turn off your IMs, Slack, Hipchat, email, phones... seriously

Multitasking does NOT work (for work which requires focus)[^1]

[^1]: https://blog.codinghorror.com/the-multi-tasking-myth, http://amzn.to/2ojSBzx and http://amzn.to/2oTZSDU

---

# Process

* Lectures, demos and hands-on labs - you'll download them soon
* Lunch break 12-1pm and 2 smaller breaks before and after
* Fill out the sign up sheets and DI evaluation *before* you leave (put in the envelope)
* Slides are often just talking points because reading from the slides is boring so pay attention and take notes!
* Labs have detailed step by step walk-through

---

# Questions

* General questions - ask during the open frame, NOT during the lecture (write it down to remember later)
* Specific questions (why XYZ is not working on my computer!?) - ask during labs

---

# Table of Contents

---

## Module 1: Cloud and AWS Basics

* Why cloud?
* Overview of cloud computing
* Main concepts: Regions and AZs
* Main AWS Services: EC2, S3, EBS, VPC, Glacier, CloudWatch, Alerts
* Billing and calculator
* Lab 0: Installs

---

## Module 2: Main EC2 Concepts

* Images
* Types, IAM and User Data
* Storage
* Tags

---

## Module 2: Main EC2 Concepts (cont)

* Key pairs
* Security groups
* ELB, Elastic IP, VPC and subnets
* Stop vs terminate

---

##  Module 2: Launching EC2

* Demo: Launching EC2
  * Launching EC2: images, types, storage, tags
  * Creating security groups
  * Working with SSH key pairs
  * Connecting to EC2
* Lab 1: Create an instance with WordPress, connect to it and deploy code

---

# Module 3: Environment and App Deploy Automation

* User Data
* Demo: User Data for Apache httpd and HTML page
* Demo: User Data for a Node app with pm2 (restart on reboot)
* Demo: Pulling code from S3, and GitHub
* Lab 2: Launching hello world

---

## Module 4: Networking

* VPC
* Interface
* Subnets
* ELB
* Elastic IP
* Demo: Create ELB and 2 EC2 instances with Apache httpd, make one fail - see the other running
* Lab 3: Create ELB and 2 EC2 instances with Apache httpd

---


## Module 5: S3

* Buckets
* HTTP access
* IAM Roles
* Versioning and multi-region
* Demo: Upload an object to S3 bucket via web console
* Lab 4: Server an HTML page from S3

---

## Module 6: Auto Scaling

* Alerts and CloudWatch
* Demo: Create a launch config, auto scaling group and policy to increase instances
* Demo: Create a launch configuration and an autoscaling group, and see if it works
* Lab 5: Deploy 2 Node apps under ELB, then load test it to see if autoscaling works

---

## Outro

* Summary
* AWS Events
* AWS Certifications
* AWS Books
* AWS Courses
