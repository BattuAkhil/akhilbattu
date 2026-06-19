Successfully Migrated WordPress to a New #AWS #LightsailInstance!
I recently completed a manual migration of a WordPress site from one Lightsail instance to another (Bitnami stack). Along the way, I got to work deeply with both the frontend and backend components of Bitnami’s stack, covering Apache, MariaDB, PHP, Varnish, and of course, WordPress itself.
🔑 Key steps I followed:
📂 Backed up essential WordPress files (wp-content, wp-config.php, .htaccess, wp-includes, wp-admin).
🗄️ Exported the database with mysqldump and securely transferred both files & DB backups via scp.
⚙️ Restored backups on the new Lightsail instance, adjusted database credentials in wp-config.php, and set correct permissions/ownership (bitnami:daemon).
🔄 Fixed common post-migration issues:
Missing/corrupted theme → switched to default theme.
Image/media upload errors → corrected uploads folder permissions.
Old domain references → updated siteurl, home, and wp_posts with the new domain.
Elementor/style conflicts → disabled Bitnami PageSpeed caching.
💡 Key learnings / fixes achieved:
Avoiding the dreaded white screen / PHP fatal errors after migration.
Restoring access when admin login credentials were broken.
Fixing 403/404 errors caused by permissions and domain mismatches.
Understanding how Bitnami bundles & manages its stack internally (ctlscript.sh, bncert-tool, etc.).
This experience reinforced the importance of:
 ✅ Knowing what files + database tables are essential.
 ✅ Setting correct permissions after migration.
 ✅ Double-checking domain + cache configurations to avoid styling/layout issues.
🔧 Next up: automating this migration with scripts and exploring AWS Snapshots and CloudFormation for faster provisioning.
👉 If you’ve faced tricky WordPress migrations, how did you solve the theme/plugin issues?









🚀** Migrating a Bitnami WordPress Stack Between AWS Accounts (Lightsail → EC2 → Lightsail)**
My recent hands-on migration breakdown
I recently completed a full WordPress Bitnami stack migration across AWS accounts — including Apache, PHP, MySQL, SSL, configs, and application data.
 Here’s the exact workflow I used 👇
🧰 Tech Stack
OS: Ubuntu
Web Server: Apache
Database: MySQL
Language: PHP
Platform: Bitnami WordPress (Lightsail)
📁 Key Bitnami File Paths
Frontend:
 wordpress/, phpmyadmin/, wp-cli/, bncert, stats/
Backend:
 apache/, mysql/, mariadb/, php/, varnish/, nami/, var/, scripts/
Important files:
/opt/bitnami/apache2/conf/httpd.conf → Apache config
/opt/bitnami/mysql/data/ → DB files
/opt/bitnami/wordpress/ → WP core
/home/bitnami/.ssh/authorized_keys → SSH access
/home/bitnami/bitnami_application_password → DB+admin password
💾 Backup Strategy
🔹 1. Database Backup
mysqldump -u root -p --all-databases > backup.sql
🔹 2. WordPress Essential Files
sudo tar -czvf wordpress-essential-backup.tar.gz wp-content/ wp-config.php .htaccess wp-includes wp-admin
🔹 3. Transfer Files (Local ↔ Server)
scp -i key.pem user@IP:/home/bitnami/file.zip ~/Downloads/
🛫 Lightsail → EC2 Migration
Step 1: Create Snapshot
Lightsail → Create Snapshot → Export to EC2 AMI
Step 2: Share AMI with Recipient AWS Account
Add IAM policy allowing AMI + S3 operations.
Step 3: Launch EC2 from Shared AMI
Use same volume structure as original Lightsail instance.
🔄 EC2 → New Lightsail Instance
Since AWS doesn't support direct import back into Lightsail:
Option B: Manual Migration (Best Practice)
1️⃣ Create new Lightsail instance
 2️⃣ Install Bitnami WordPress
 3️⃣ Transfer backups from S3/SCP
 4️⃣ Restore DB + WordPress files
 5️⃣ Reconfigure DNS + SSL
 6️⃣ Restart services

sudo /opt/bitnami/ctlscript.sh restart
🔧 Database Restore
sudo mysql -u root -p wordpress < ~/database-backup.sql
Create missing DB:
CREATE DATABASE wordpress;
🌐 WordPress User Recovery via SQL
INSERT INTO wp_users (...) VALUES ('wpuser', MD5('admin@123'), ...);
🧵 Theme Fix (DB)
UPDATE wp_options SET option_value='twentytwentyfour' WHERE option_name IN ('template', 'stylesheet');
🔐 IAM Policy:
lightsail:*,ec2:* (AMI operations),s3:*
iam:PassRole
🧩 Key Learnings
✔ Bitnami stacks are self-contained — configs + services in /opt/bitnami
 ✔ Migration ≠ copying WordPress folder; DB + configs are mandatory
 ✔ SSL, SSH keys, .env, custom configs are often overlooked
 ✔ Direct Lightsail import is not possible → manual migration required
 ✔ Permissions matter (bitnami:daemon + 775)
 
 
 
 
 
 
 
 
 
 
 
 
 
** automated version for migration #but more #drawbacks**
🚀 Migrating WordPress on Lightsail – Step by Step
💻 Stack: Ubuntu | Apache | MySQL | PHP | Bitnami
 🛠️ Tools: WP-CLI, bncerttool, ctlscript.sh
Migration Made Easy:
1️⃣ Create a Lightsail snapshot → export to EC2 AMI → share with target account
 2️⃣ Launch new instance → fetch backup from S3
 3️⃣ Restore database & WordPress files
 4️⃣ Fix permissions & restart services ✅
Quick Tips:
📦 Backup: wp-content, wp-config.php, .htaccess, DB
 🔒 Keep SSL certificates ready
 🎨 Switch themes / create admin users via SQL if needed
Outcome:
 Smooth migration ✅ Minimal downtime ⏱️#AWS #Lightsail #WordPress #Bitnami #Migration #CloudComputing
