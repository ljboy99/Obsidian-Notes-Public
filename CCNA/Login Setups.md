You can enable local logins by going into global configuration mode (configure terminal) and then establishing a username and password
```
username user password pass
```
Where user and pass are the actual username and password you're setting up.

You also need to tell the device to require a login for access. 
While in global configuration mode, you need to type in 'line con 0' and then enter 'login local' for the device to require locally stored credentials.