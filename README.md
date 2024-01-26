# Eval_AWS
### login to AWSlab, craete an instance with the security group with the rules ssh, http, https and create elasticIP
### download labsuser.pem 
### open the console in the path where I have saved the file with command
  ssh -i labsuser.pem ubuntu@elasticIP
### Install mysql and php after doing an updates
  sudo apt-get update
  sudo apt-get install mysql-server php libapache2-mod-php php-mysql
### Install the aplication with the provided URL and unzip
  wget -U "Firefox" "https://phpgurukul...." -O hostel.zip
  sudo apt-get install unzip
  sudo unzip hostel.zip
### Rename system manager directory to Hoste_Man
  mv Hostel\ management\ System\ Project/ Hostel_Man
### Activate the mysql service and configured it so that it doesn´t ask for the password every time
  sudo service mysql start
  mysql -u root -p
  use mysql;
  update user set plugin='myqsl_native_password' where User='root';
  flush privileges;
  exit;
### Go to directory home and update changes in mysql 
  cd ~
  sudo service mysql restart
### Go to directory Hostel_man and move the hostel directory inside to /var/www/html
  cd Hostel_Man 
  sudo mv hostel/ /var/www/html
### Search in Hostel_Man the dir SQL File/ and enter inside to move the hostel.sql to the home of the instance
  cd Hoste_Man 
  ll
  cd SQL File 
  sudo mv hostel.sql ~
### Enter into mysql create hostel database and insert the data from tables with the file hostel.sql
  sudo service mysql start
  mysql -u root -p
  create database hostel;
  source /home/ubuntu/hostel.sql
  show tables;
  exit;
### Create the .conf file the necessary that we will copy from 000-default.conf to leave this as original and enabled the one we have configured with the new route and IP
  cd /etc/apache2/sites-enabled
  cp 000-default.conf 001-midefaut.conf
  sudo nano 001-midafaut.conf--> ServrName 44.216.110.185, DocumenRoot /var/www/html/hostel
  sudo a2ensite 001-midefaut.conf
  sudo a2dissite 000-default.conf
  sudo service apache2 restart
### Finaly to check that we have deployed the application by entering the elastic IP in the browser
  44.216.110.185 
