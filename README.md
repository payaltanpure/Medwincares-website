User Manual
Topic: Cloud-Based Hospital Management System Using AWS EC2

Step 1: CONNECT TO EC2 (RUN ON YOUR PC)
Command:
ssh -i "E:\bedse\6th sem\cc\payal.pem" ubuntu@<EC2-IP>
Meaning:
ssh → Secure Shell used to connect remote server
-i → identity file (private key file .pem)
ubuntu@IP → EC2 username and public IP address
Purpose:
Used to remotely access AWS EC2 server from local system.

Step 2: UPDATE SERVER PACKAGES (RUN IN EC2)
Command:
sudo apt update -y
Meaning:
apt update → updates list of available software packages
-y → automatically confirms updates
Purpose:
Refreshes system package database before installing software.

Step 3: INSTALL APACHE SERVER
Command:
sudo apt install apache2 -y
Meaning:
Installs Apache web server software on EC2
Purpose:
Used to host and run web applications in browser.



Step 4: INSTALL MYSQL SERVER
Command:
sudo apt install mysql-server -y
Meaning:
Installs MySQL database management system
Purpose:
Used to store and manage backend application data.

Step 5: INSTALL PHP
Command:
sudo apt install php libapache2-mod-php php-mysql -y
Meaning:
php → backend scripting language
php-mysql → connects PHP with MySQL database
libapache2-mod-php → allows Apache to run PHP files
Purpose:
Enables dynamic web application functionality.

Step 6: START SERVICES
Command:
sudo systemctl start apache2
sudo systemctl start mysql
Meaning:
systemctl → controls system services
start → runs the service immediately
Purpose:
Activates web server and database services.




Step 7: ENABLE AUTO START SERVICES
Command:
sudo systemctl enable apache2
sudo systemctl enable mysql
Meaning:
enable → starts services automatically after system reboot
Purpose:
Ensures services run even after server restart.

Step 8: UPLOAD PROJECT FROM PC TO EC2
Command:
scp -i "E:\bedse\6th sem\cc\payal.pem" -r "C:\xampp\htdocs\medwincares" ubuntu@<EC2-IP>:/home/ubuntu/
Meaning:
scp → secure copy command for file transfer
-r → copy folder recursively
source → local system project path
destination → EC2 server path
Purpose:
Transfers project files from local system to cloud server.

Step 9: MOVE PROJECT TO APACHE DIRECTORY (RUN IN EC2)
Command:
sudo mv /home/ubuntu/medwincares /var/www/html/
Meaning:
mv → move command used to shift files
/var/www/html/ → default Apache web directory
Purpose:
Makes project accessible through browser.



Step 10: SET FILE PERMISSIONS
Command:
sudo chmod -R 755 /var/www/html/medwincares
Meaning:
chmod → changes file permissions
755 → read and execute access
-R → applies changes to all files and folders
Purpose:
Allows web server to access project files.

Step 11: CHANGE OWNERSHIP
Command:
sudo chown -R www-data:www-data /var/www/html/medwincares
Meaning:
chown → changes file owner
www-data → Apache web server user
Purpose:
Gives Apache permission to manage website files.

Step 12: LOGIN TO MYSQL
Command:
mysql -u root -p
Meaning:
-u → username
-p → password prompt
Purpose:
Used to access MySQL database system.




Step 13: CREATE DATABASE
Command:
CREATE DATABASE hospital_db;
Meaning:
Creates a new database named hospital_db
Purpose:
Stores all application data.

Step 14: IMPORT DATABASE FILE
Command:
mysql -u hospital_user -p hospital_db < /home/ubuntu/hospital.sql
Meaning:
< → imports SQL file into database
hospital.sql → database backup file
Purpose:
Loads tables and data into MySQL database.

Step 15: RESTART APACHE SERVER
Command:
sudo systemctl restart apache2
Meaning:
Restarts Apache web server
Purpose:
Applies all configuration and code changes.

Step 16: OPEN WEBSITE
Command / URL:
http://<EC2-IP>/medwincares
Meaning:
Opens deployed hospital management system in browser

Purpose:
Used to access live cloud-hosted website.

ERROR FIXES 

Error 1: DATE FORMAT ERROR
Command / Fix:
$date = date('Y-m-d', strtotime($_POST['date']));
Meaning:
Converts date into MySQL standard format (YYYY-MM-DD)
Purpose:
Prevents invalid date insertion error.

Error 2: TIME FORMAT ERROR
Command / Fix:
$time = date("H:i:s", strtotime($_POST['time']));
Meaning:
Converts time into 24-hour format
Purpose:
Ensures MySQL accepts time values correctly.

Error 3: CITY TYPE ERROR
Command:
ALTER TABLE registration MODIFY city VARCHAR(100);
Meaning:
Changes column type from integer to string
Purpose:
Allows text like city names (Pune, Mumbai).


Error 4: PERMISSION ISSUE
Command:
sudo chmod -R 755 /var/www/html/medwincares
Meaning:
Fixes file access permissions
Purpose:
Allows Apache to read project files.

Error 5: PHPMailer NOT FOUND
Command:
scp -r PHPMAILER ubuntu@<EC2-IP>:/home/ubuntu/
Meaning:
Uploads missing mail library
Purpose:
Enables email functionality in project.












