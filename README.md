<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Visualize a Relational Database

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-databases-rds)

**Author:** R  


---

## Visualise a Relational Database

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-databases-rds_1fddb0b5)

---

## Introducing Today's Project!

### What is Amazon RDS?

Amazon RDS (Relational Database Service) is a managed service from AWS that makes it easier to set up, operate, and scale relational databases in the cloud. It handles routine database tasks like provisioning, backups, patch management, and scaling.

### How I used Amazon RDS in this project

In today’s project, I used Amazon RDS to create a database (QuickSightDatabase) to store data and connect it to Amazon QuickSight for visualizing that data in charts and dashboards.

### One thing I didn't expect in this project was...

One thing I didn’t expect was the need to set up and configure several security layers (VPC, security groups, IAM roles) for secure communication between QuickSight and RDS, especially the troubleshooting with permissions for the VPC connection.

### This project took me...

This project took me approximately 2 hours to complete, including setup, troubleshooting, and final testing of the connection between RDS and QuickSight.

---

## In the first part of my project...

### Creating a Relational Database

I created my relational database by using Amazon RDS with the Easy Create option, selecting MySQL as the engine, choosing the free tier, setting the DB identifier to QuickSightDatabase, and configuring credentials manually before launching.

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-databases-rds_43343546)

---

## Understanding Relational Databases

A relational database is a structured database that organizes data into tables with rows and columns, where relationships between data are maintained using keys. It allows efficient querying and management of data using SQL.

### MySQL vs SQL

The difference between MySQL and SQL is that SQL is a language used to query and manage relational databases, while MySQL is a specific relational database management system (RDBMS) that uses SQL to store, retrieve, and manipulate data.

---

## Populating my RDS instance

The first thing I did was make my RDS instance public because MySQL Workbench runs on my local machine, outside of AWS, and needs network access to connect to the RDS instance. This allows external tools to reach the database over the internet.

I had to update the default security group for my RDS schema because it controls which traffic can access the database. By adding an inbound rule for my IP, I allowed MySQL Workbench on my local machine to securely connect to the RDS instance.

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-databases-rds_91b9fd1g)

---

## Using MySQL Workbench

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-databases-rds_1fddb0b5)

To populate my database, I created two tables in MySQL Workbench using SQL commands, then inserted sample employee and department data into them using `INSERT INTO` statements, and confirmed the data was loaded using `SELECT` queries.

---

## Connecting QuickSight and RDS

To connect my RDS instance to QuickSight I updated the security group to allow all inbound traffic, then in QuickSight I added a new dataset, selected RDS, entered my instance details and credentials, and validated the connection.

This solution is risky because our RDS instance is publicly accessible to the entire internet via 0.0.0.0/0, which exposes it to potential unauthorized access, data breaches, and malicious attacks.

### A better strategy

First, I made a new security group so that QuickSight could securely connect to my RDS instance without making the database publicly accessible, allowing only authorized traffic from QuickSight within the same VPC.

I connected my new security group to QuickSight by creating a VPC connection using the same VPC and security group, then updated the execution role with the required permissions through an inline IAM policy to allow QuickSight to access the network.

---

## Now to secure my RDS instance

To secure my RDS instance, I made the database not publicly accessible by modifying its settings. Then, I created a dedicated RDS security group and added inbound rules allowing access only from the QuickSight security group for proper isolation.

I made sure that my RDS instance could be accessed from QuickSight by attaching the newly created RDS security group to the instance, adding inbound rules to allow access specifically from the QuickSight security group, and applying the changes.

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-databases-rds_1709b26b)

---

## Adding RDS as a data source for QuickSight

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-databases-rds_1709b29b)

This data source is different from my initial data source because it is connected securely through a VPC, using the RDS_VPC connection type instead of a public network. This ensures that the connection is private and protected from external access.

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-databases-rds_1709b30b)

---

---
