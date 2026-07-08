# WordPress Migration on AWS Lightsail (Bitnami Stack)

## Project Overview

This project documents a complete migration of a **Bitnami WordPress** application between AWS environments, including **AWS account migration**, **Lightsail-to-EC2 export**, and **manual restoration to a new Lightsail instance**.

The migration involved transferring the application, database, web server configuration, SSL configuration, and application data while minimizing downtime and ensuring data integrity.

The project also covers troubleshooting common migration issues such as broken themes, media upload failures, permission errors, database inconsistencies, and domain configuration.

> **Note:** Sensitive information such as public IP addresses, domain names, SSH keys, and account identifiers has been removed from this documentation for security purposes.

---

# Technologies Used

## Cloud Platform

* AWS Lightsail
* Amazon EC2
* Amazon S3
* AWS IAM

## Operating System

* Ubuntu Linux

## Web Stack

* Apache HTTP Server
* PHP
* MariaDB / MySQL
* Bitnami WordPress
* Varnish Cache

## Tools

* SSH
* SCP
* mysqldump
* MySQL Client
* WP-CLI
* bncert-tool
* Bitnami ctlscript.sh

---

# Migration Architecture

```text
Original AWS Account
──────────────────────────────────────────

AWS Lightsail
(Bitnami WordPress)
        │
        ├── WordPress Files
        ├── MySQL Database
        ├── Apache Configuration
        ├── SSL Certificates
        └── Application Configuration
                │
                ▼
         Lightsail Snapshot
                │
                ▼
          Export to EC2 AMI
                │
                ▼
        Share AMI Across AWS Accounts
                │
                ▼

Destination AWS Account
──────────────────────────────────────────

Amazon EC2
      │
      ▼
Backup Extraction
      │
      ▼
Amazon S3 / SCP Transfer
      │
      ▼
New AWS Lightsail Instance
(Bitnami WordPress)
      │
      ▼
Database Restore
      │
      ▼
Application Restore
      │
      ▼
DNS + SSL Configuration
      │
      ▼
Production Ready
```

---

# Project Objectives

* Migrate WordPress across AWS accounts.
* Preserve application data and configuration.
* Minimize service downtime.
* Restore a fully functional Bitnami environment.
* Troubleshoot common migration issues.
* Document a repeatable migration workflow.

---

# Components Migrated

## Application Files

Migrated essential WordPress components including:

* wp-content
* wp-admin
* wp-includes
* wp-config.php
* .htaccess

---

## Database

Database migration included:

* Full MySQL dump
* Database restoration
* User validation
* Site URL updates
* Content verification

---

## Bitnami Configuration

Migrated and validated:

* Apache configuration
* PHP configuration
* MariaDB services
* Varnish configuration
* SSL configuration
* Application services

---

# Backup Strategy

## Database Backup

Created a full MySQL database export before migration.

## Application Backup

Archived essential WordPress files while preserving permissions and configuration.

## Secure File Transfer

Transferred backups securely using SSH and SCP between environments.

---

# Migration Workflow

## Phase 1

* Create Lightsail Snapshot
* Export Snapshot as EC2 AMI
* Share AMI with destination AWS account

## Phase 2

* Launch EC2 instance
* Validate application
* Extract required data

## Phase 3

* Create new Bitnami WordPress Lightsail instance
* Transfer application backup
* Restore WordPress files
* Restore database

## Phase 4

* Update configuration
* Configure DNS
* Install SSL
* Restart services
* Validate application

---

# Troubleshooting Performed

During migration, several common WordPress issues were identified and resolved.

### Theme Recovery

* Switched to default WordPress theme
* Corrected theme configuration

### Media Upload Issues

* Fixed uploads directory permissions
* Restored ownership
* Verified Apache permissions

### Domain Migration

Updated:

* siteurl
* home
* Internal database references

### Authentication Recovery

Recovered administrator access through SQL when required.

### Permission Fixes

Configured proper ownership using:

* bitnami
* daemon

Corrected directory permissions to restore application functionality.

### Performance Issues

Disabled unnecessary Bitnami PageSpeed caching during migration to resolve styling and caching conflicts.

---

# Bitnami Components Explored

This project provided practical experience with:

* Apache
* MariaDB
* PHP
* Varnish
* WP-CLI
* bncert-tool
* ctlscript.sh
* Bitnami application structure

---

# Security Considerations

* Secure SSH-based file transfer
* IAM-controlled AMI sharing
* Restricted access using security groups
* SSL certificate reconfiguration
* Sensitive configuration files protected
* Least-privilege access

---

# Key Learning Outcomes

* Understanding the internal structure of Bitnami WordPress.
* Migrating complete WordPress applications beyond simply copying files.
* Managing database backup and restoration.
* Troubleshooting common migration failures.
* Configuring permissions and ownership correctly.
* Working with AWS Lightsail snapshots and EC2 AMIs.
* Managing SSL certificates after migration.
* Designing migration workflows with minimal downtime.

---

# Current Limitations

* AWS does not support importing EC2 AMIs directly into Lightsail.
* Manual restoration is required for Lightsail migrations.
* SSL certificates typically require reconfiguration after migration.
* Environment-specific configuration files must be reviewed manually.
* DNS propagation time may temporarily affect availability.

---

# Future Enhancements

* Automate migrations using Bash scripts.
* Integrate AWS Systems Manager (SSM).
* Store backups automatically in Amazon S3.
* Automate snapshot creation with AWS Lambda.
* Provision infrastructure using Terraform or CloudFormation.
* Build a CI/CD pipeline for automated deployments.
* Add monitoring using CloudWatch and Grafana.
* Reduce migration downtime through blue-green deployment strategies.

---

# Skills Demonstrated

* AWS Lightsail
* Amazon EC2
* WordPress Administration
* Bitnami Stack
* Linux Administration
* Apache
* MariaDB
* PHP
* MySQL Backup & Recovery
* SSH & SCP
* AWS IAM
* Disaster Recovery
* Migration Planning
* Cloud Infrastructure
* Troubleshooting
* DevOps Practices

---

# Conclusion

This project provided practical experience in planning and executing a complete WordPress migration across AWS environments. It reinforced the importance of backup strategies, secure data transfer, infrastructure understanding, and systematic troubleshooting while demonstrating how production workloads can be migrated with minimal downtime and maintained through repeatable operational processes.

Implementation Commands
1. Create a Database Backup
mysqldump -u root -p wordpress > wordpress-backup.sql

Or backup all databases:

mysqldump -u root -p --all-databases > full-backup.sql
2. Backup WordPress Files
cd /opt/bitnami

sudo tar -czvf wordpress-backup.tar.gz \
wordpress \
apache2/conf \
php \
varnish

Or backup only the essential WordPress files:

cd /opt/bitnami/wordpress

sudo tar -czvf wordpress-essential.tar.gz \
wp-content \
wp-admin \
wp-includes \
wp-config.php \
.htaccess
3. Transfer Backup to Another Server
scp -i lightsail.pem \
wordpress-backup.tar.gz \
bitnami@NEW_SERVER_IP:/home/bitnami/

Transfer database backup:

scp -i lightsail.pem \
wordpress-backup.sql \
bitnami@NEW_SERVER_IP:/home/bitnami/
4. Restore WordPress Files
cd /opt/bitnami

sudo tar -xzvf /home/bitnami/wordpress-backup.tar.gz
5. Restore Database
mysql -u root -p wordpress < wordpress-backup.sql

If the database does not exist:

CREATE DATABASE wordpress;

Then restore:

mysql -u root -p wordpress < wordpress-backup.sql
6. Update WordPress Configuration

Edit:

sudo nano /opt/bitnami/wordpress/wp-config.php

Update:

define('DB_NAME', 'wordpress');
define('DB_USER', 'root');
define('DB_PASSWORD', 'your-password');
define('DB_HOST', 'localhost');
7. Fix File Permissions
sudo chown -R bitnami:daemon /opt/bitnami/wordpress

sudo find /opt/bitnami/wordpress -type d -exec chmod 775 {} \;

sudo find /opt/bitnami/wordpress -type f -exec chmod 664 {} \;
8. Restart Bitnami Services
sudo /opt/bitnami/ctlscript.sh restart

Check service status:

sudo /opt/bitnami/ctlscript.sh status
9. Update Domain References

Login to MySQL:

mysql -u root -p

Update URLs:

UPDATE wp_options
SET option_value='https://new-domain.com'
WHERE option_name IN ('siteurl','home');
10. Create a New Admin User (Recovery)
INSERT INTO wp_users
(user_login,user_pass,user_nicename,user_email,user_status,display_name)
VALUES
('admin', MD5('StrongPassword123'),
'admin','admin@example.com',0,'Administrator');

Grant administrator role:

INSERT INTO wp_usermeta
(user_id,meta_key,meta_value)
VALUES
(1,'wp_capabilities','a:1:{s:13:"administrator";b:1;}');
11. Switch to Default Theme
UPDATE wp_options
SET option_value='twentytwentyfour'
WHERE option_name IN ('template','stylesheet');
12. Disable Bitnami PageSpeed (If Required)
sudo nano /opt/bitnami/apache2/conf/httpd.conf

Comment or disable the PageSpeed module, then restart Apache:

sudo /opt/bitnami/ctlscript.sh restart
13. Verify Apache & MySQL
curl -I http://localhost
systemctl status apache2
mysql -u root -p
14. Verify WordPress Installation
wp core version

List installed plugins:

wp plugin list

List installed themes:

wp theme list
Migration Validation Checklist

After the migration, verify:
✅ WordPress home page loads correctly
✅ Admin dashboard is accessible
✅ Database connection is successful
✅ Images and media files display correctly
✅ Theme and plugins function properly
✅ SSL certificate is active
✅ File permissions 
