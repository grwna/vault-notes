# How to Detect
Testing for SQLi, submit these:
- The single quote character `'` and look for errors or other anomalies.
- Some SQL-specific syntax that evaluates to the base (original) value of the entry point, and to a different value, and look for systematic differences in the application responses.
- Boolean conditions such as `OR 1=1` and `OR 1=2`, and look for differences in the application's responses.
- Payloads designed to trigger time delays when executed within a SQL query, and look for differences in the time taken to respond.
- OAST payloads designed to trigger an out-of-band network interaction when executed within a SQL query, and monitor any resulting interactions.

# Occurence
Most SQLi Vuln is within the `WHERE` clause of a `SELECT` query, but it can happen to other parts, like `INSERT`-ed values, updated values etc.
Think about the parts of a query that often uses user input. 

# Injection
You will often use `--` in the query to avoid syntax error due to deformed syntax after injection. Keep in mind that mostly you won't be able to inject `SELECT` statements directly.

>[!important]
>In MySQL, the comment mark '--' has to be followed by a space to work as comment. If your payload doesn't work, it might be because of this. As a safe rule, just always add space to the comments. 

>[!Tip]
>Use Burp Repeater to test out payload.
# UNION Attacks
Used to do `SELECT` statements from different tables.
**Conditions for UNION**
In order for the UNION attack to work, these conditions must be met:
- The number of columns of the two queries must be the same
- The data types for each column must be compatible
This means it is beneficial to have less columns.

#### Detecting Number of Columns
**ORDER BY**
One way to detect number of columns returned by a query is injecting `ORDER BY` clauses by **index**. Here are possible payloads:
- `' ORDER BY 1--`
- `' ORDER BY 2--`
- `' ORDER BY 3--`
- 
You would send these payloads and see the response from the server. If there are any error or difference in response, it might be because the index doesn't exist.

**UNION SELECT NULL**
- ' UNION SELECT NULL-- 
- ' UNION SELECT NULL,NULL-- 
- ' UNION SELECT NULL,NULL,NULL--

This works because `NULL` is compatible with any column data types.
>[!Database Specific Injection]
>Different databases can have different syntax. This can cause variations of what you need/can
>inject. There is a [cheatsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet) available for this by PortSwigger.

#### Detecting Column's Datatype
- ' UNION SELECT 'a',NULL,NULL,NULL-- 
- ' UNION SELECT NULL,'a',NULL,NULL-- 
- ' UNION SELECT NULL,NULL,'a',NULL-- 
- ' UNION SELECT NULL,NULL,NULL,'a'--

The payload like above can be used to probe each column index datatype compatibility. In the example above, we probe each column to see which ones is compatible with string.

#### Retrieving Data
 Now you can retrieve contents of a different table. let's say `users` with columns `username` and `password`. However, in a blackbox setting, you won't know the table's and column's name. Databases provides ways to see tables that exists in the database.

>[!Tip]
>If the base query only allows for one column of string, how can you retrieve data from multiple columns?
>
>You can do this by using string concatenation to trick the query to returning a single column with multiple values.

# Examining Database 
- Get the type and version of the database software.
- Tables and columns inside the database.

Using version queries (which you can read in the [cheatsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)), you can read information about the database software. 

You can craft a UNION attack payload with these version queries.

You can also do similar operations for retrieving the **contents** of a database.
The general query is: `SELECT * FROM information_schema.tables`.

Some attributes of `information_schema` that might be useful:
- `tables`
- `columns`
- `schemata`
- `user_privileges`
- `routines`
- `views`

# Blind SQLi
HTTP responses does not contain any results that are relevant to the SQL query (no errors, etc.). This renders `UNION` attacks useless. Other techniques must be used.

Sometimes even if the response aren't relevant, behaviours of the app may change based on the Query. 

We can use the behaviour response with brute-forcing techniques to obtain a secret. For example:
```
xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 'm
```
This query returns whether the first character of the password is larger than m. If it is, then it returns true and the app may behave a certain way.

>[!note]
>You can use a python script to automate attacks like these

**Variations of these challenges**
- **Error based** - error messages may reveal something
	- Database errors (so we dont depend on if data returned is empty or not)
		- **Example payload**: `xyz' AND (SELECT CASE WHEN (Username = 'Administrator' AND SUBSTRING(Password, 1, 1) > 'm') THEN 1/0 ELSE 'a' END FROM Users)='a` (NOTE: different DB's might require different syntax)
		- You can see this is similar to normal conditional based SQLi, but we exploit `1/0` to cause DB error
		
- **Verbose Error Messages Leak**
	- Yeah basically the error messages reveal too much, you know how this could be dangerous
	- **Payload**: `CAST((SELECT example_column FROM example_table) AS int)`
	- Example: with CAST keyword, if you cast a string to integer you may get the error:
	- `ERROR: invalid input syntax for type integer: "Example data"`
	- Where "Example Data" is the value of the column youre trying to leak

- **Time Delays**
	- Trigger time delays based on conditionals, which delays the HTTP response
	- **Payload**: '; `IF (SELECT COUNT(Username) FROM Users WHERE Username = 'Administrator' AND SUBSTRING(Password, 1, 1) > 'm') = 1 WAITFOR DELAY '0:0:{delay_amount}'--`
	- The payload above is Microsoft db syntax

# Blind SQLi with OAST