# Authentication
## Username Enumeration
In the login page we can tell some things. For example, you can try registering usernames. If the app says "username already taken", this means you obtained a valid username.
We can do this many times for many usernames to get a list of valid usernames to use to gain access to the app.

## Bypassing 2FA
Sometimes when asked for 2FA you might already be logged in, and the 2FA step can be skipped entirely if the implementation is bad.

# SSRF
(More: [[SSRF]])
Cause the server to connect to unintended locations, which can leak sensitive data. This can be done against the server (server connect to internal service) or external.
## SSRF Against the Server
Done by supplying `localhost` URL to the server. The server will request/fetch data from such URL and can leak data (i.e. if the server fetch data from `localhost/admin` then contents of `admin` can be leaked).

Keep in mind this can only happen if the server is allowed to have full access to the local machine, which makes this vulnerability critical.

## SSRF Against Other Backend Service
Practically the same as server, but this time not to the localhost.

# File Upload Vuln
[[File Upload Vulnerabilities]]
When users are allowed to upload files. There need to be restrictions on the types, names, etc. of the files. Failing to do so may allow hackers to cause harm by RCE or other danger caused by the file upload.
**RCE**
Some attacks upload files, then send a follow up HTTP request to trigger the execution of the file.

## Unrestricted File Upload to Deploy Web Shell
>[!Web Shell]
>A web shell is a malicious script that enables an attacker to execute arbitrary commands on a remote web server simply by sending HTTP requests to the right endpoint. This practically give you all access.

A web shell can be spawned by sending backend files that can be executed, like PHP, Java, or Python.

Example of web shell payload (PHP):
- `<?php echo file_get_contents('/path/to/target/file'); ?>`
- `<?php echo system($_GET['command']); ?>`

## Flawed File Type Validation
For sending data through HTML forms,  the content type `multipart/form-data` is used. WIth multi part data, each data can have their own content type, for example `image/jpeg`. Some flawed validation might check the content type but not the actual data. 

# OS Command Injection
Allows user to inject shell commands which many times give access to the OS and other services connected to it.

**Useful Commands**

| Purpose of command    | Linux         | Windows         |
| --------------------- | ------------- | --------------- |
| Name of current user  | `whoami`      | `whoami`        |
| Operating system      | `uname -a`    | `ver`           |
| Network configuration | `ifconfig`    | `ipconfig /all` |
| Network connections   | `netstat -an` | `netstat -an`   |
| Running processes     | `ps -ef`      | `tasklist`      |
Make sure your payload is in this form 
```
& echo aiwefwlguh &
```
The last `&` is there to make sure the command isnt polluted with other tokens.

# SQLi
(more: [[SQLi]])
Tipically, the most basic [[SQLi]] have to do with quotation and how they can end or cut queries done by the server. You can also use command mark `--` in conjunction.

Example, with query
`SELECT * FROM products WHERE category = '{input}' AND released = 1`
You can input `Gifts' OR 1=1 --'` with the comment to ignore the AND part of the query.

You can use this attack to skip a password check for example, if the system uses SQL for authentication (bruh)