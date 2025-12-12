# MySQL Install + User Creation (One-Line Commands + Explanation)

sudo apt update                       # Update package list
sudo apt install mysql-server -y      # Install MySQL server
sudo systemctl start mysql            # Start MySQL service
sudo systemctl enable mysql           # Enable MySQL to auto-start on boot
sudo mysql_secure_installation        # Run MySQL security setup
sudo mysql                            # Log into MySQL as root
mysql -u root -p                      # Log into MySQL using the root user and prompt for password

CREATE USER 'koko'@'%' IDENTIFIED BY 'koko2026';      # Create user koko with password, allow any host
GRANT ALL PRIVILEGES ON *.* TO 'koko'@'%' WITH GRANT OPTION;   # Give full permissions
FLUSH PRIVILEGES;                                      # Apply permission changes
EXIT;                                                  # Exit MySQL shell



### ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


### Login to MySQL as root
# Login to MySQL as root user (will prompt for password)
mysql -u root -p  

### Login to MySQL as k-user
# Login to MySQL as k user (will prompt for password)
mysql -u k -p 

### Create a database
# Create a new database named 'my_database' with UTF8MB4 character set and Unicode collation
CREATE DATABASE my_database CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;  

### Create a new user 'k' that can connect from any host (%) with a password
# Uses the default authentication plugin (caching_sha2_password in MySQL 8+)
CREATE USER 'k'@'%' IDENTIFIED BY 'StrongPassword123';  
                                        
### Create a new user
# Create a new user 'k' that can connect from any host (%) using mysql_native_password plugin and set password
CREATE USER 'k'@'%' IDENTIFIED WITH mysql_native_password BY 'StrongPassword123';  
                                       
### Grant privileges to the user
# Grant all permissions on 'my_database' database to 'k' user
GRANT ALL PRIVILEGES ON my_database.* TO 'k'@'%';  
                                        
### Apply the changes immediately
# Reload privileges so MySQL applies the changes immediately
FLUSH PRIVILEGES; 

### Check users and authentication method
# List all MySQL users, their allowed hosts, and authentication plugins
SELECT user, host, plugin FROM mysql.user;  


### **********************************************************************************************

# Inside MySQL Shell

SHOW DATABASES;                          # List all databases on the server
USE mydatabase;                          # Switch to/use a specific database
SHOW TABLES;                             # Show all tables inside the selected database
DESCRIBE users;                          # Show columns, data types, and structure of the 'users' table
SELECT * FROM users;                     # Display all data inside the 'users' table
SELECT * FROM users LIMIT 10;            # Show only first 10 rows of the table
SELECT id, name FROM users;              # Show only specific columns from a table
SHOW CREATE TABLE users;                 # Show full SQL used to create the table
CREATE DATABASE mydb;                    # Create a new database
DROP DATABASE mydb;                      # Delete a database permanently
DROP TABLE users;                        # Delete a table permanently
INSERT INTO users (name, email) VALUES ('John', 'john@gmail.com');   # Insert one row of data
UPDATE users SET name='John Doe' WHERE id=1;     # Update data for a specific row
DELETE FROM users WHERE id=1;                    # Delete a specific row from a table
EXIT;                                            # Exit the MySQL shell

                                        
