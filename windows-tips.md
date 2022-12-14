# RDP Connection
## Connecting to rdp using a rdp file
**server.rdp**
```
username:s:my-user
full address:s:x.x.x.x
password 51:b:xxxxencryptedPasswordxxxx
```
> Note: Password needs to be encrypted from the **same machine** which we intend to use the rdp file.
### Encrypting the password
#### Method 1:
Using cryptRDP5.exe from this repo https://github.com/jps-networks-modifiedOSS/openvpn-als-applications/tree/master/adito-application-rdp-xplatform-embedded/src/windows
```
cryptRDP5.exe yourpassword
```
#### Method 2:
Using PowerShell
```
("MySuperSecretPassword!" | ConvertTo-SecureString -AsPlainText -Force) | ConvertFrom-SecureString
```
### Reference
- https://serverfault.com/questions/867467/rdp-file-with-embedded-password-asks-for-password


# MySQL 8
## Resetting the root password
- Stop the Mysql process (stopping the service from services.msc or killing it from TaskManager)
- Create a init file with content similar to below and save the file to C:\mysql-init.txt
```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass';
```
- In the command prompt execute the below command.
```
mysqld --defaults-file="C:\\ProgramData\\MySQL\\MySQL Server 8.0\\my.ini" --init-file=C:\\mysql-init.txt
```
- Now the password is reset. You can delete the mysql-init.txt file and kill this mysqld invocation and start the mysqld via services.msc

### Reference
- https://dev.mysql.com/doc/mysql-windows-excerpt/8.0/en/resetting-permissions-windows.html

