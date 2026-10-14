Path traversals happens because improper sanitation, and it can cause attackers to be able to read and even write data to files (even operating system files).

Path traversals are very commonly exploited using the `../` path.
Images are sometimes stored in `/var/www/images`, allowing you to guess path.
# Obstacles
Most apps implement defenses against path traversal, but sometimes you can bypass them if they are weak. 
Examples: 
- only allows full path.
- allows nested sequences (`//`, `\/`)
- other non-recursive sanitation
- sanitation of raw strings only, allowing **URL encoding** to work
	- Sometimes you need to do double URL encoding (encode the already encoded)
- it needs to start with the expected base folder (i.e. `/var/www/images)
- it needs to have a certain file extension (you can use **null bytes** to cut off the string)
	- Example: `this\x00.jpg` might be parsed by the WAF as ending with `.jpg` but the os parses it as `this`.

# How to Prevent
The first and foremost way is to not pass user input to **filesystem APIs**, or you can make the path sanitation robust.