Allows attacker to cause server-side apps to make requests to locations, can be itself can be others in the network or that the server has access to. This can leak data, and in some cases perform arbitrary RCE.

It can also make it seem like an organization is attacking while the true attacker is masquerading as it.

# Common SSRF Attacks
SSRF exploits trust relationships of apps/services like APIs or its own system.
Usually exposed through endpoints embedded in HTTP requests.

Types 
- Against the server
	- Made possible because the access controls from server to server is not being enforced (multiple reasons why its done this way) 

- Against other back-end systems
	- Back-end systems that might be on the same network as the server or that the server has access to
