# Authentication
## Username enumeration via different responses
Go to login page, enter any username and password, catch the request in Burp Proxy, then send to intruder.

In intruder, add payload `$$` to the username field in the request. Paste the username wordlist into the payload list tab. Run a sniper attack on the username, then observe the response. After finding the correct username, do the same for the password. Voila.

## 2FA simple Bypass
Simply login to carlos, then change the URL to the homepage

# SSRF
## Basic SSRF Against Server
For some reason checkstock uses POST. Using this endpoint we can change the target url to:
```
http//localhost/admin/admin/delete?username=carlos
```

# File Upload
## Basic Web Shell
After uploading the webshell, press on the avatar and click "copy image address" then visit the address.