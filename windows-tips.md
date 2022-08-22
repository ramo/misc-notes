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
