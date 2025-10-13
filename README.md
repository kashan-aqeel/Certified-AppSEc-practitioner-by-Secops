# Certified AppSEc practitioner by-SecOps

## Input Validation Mechanisms

* What is input validation?   
Input validation is the practice of ensuring that the data received from any external source is correct, clean, and safe before your application processes it. External sources include user forms, APIs, and file uploads. Poor or missing input validation is a root cause for many common vulnerabilities, including the OWASP Top 10.

* The most important rule:   Trust no one
Never trust any data that comes from outside your application's boundaries. Always assume external data is malicious and could be trying to exploit your system. 

* Where to validate input:
  
Server-side validation: This is mandatory for security. An attacker can easily bypass validation done in the web browser (client-side) using tools like Burp Suite to change data before it reaches the server.

Client-side validation: This is for user experience, not security. It can provide immediate feedback to a user, like flagging an incorrectly formatted email address before they submit the form. 

*  The two main strategies:
  
 Allow List (Whitelisting): This is the gold standard. It defines and explicitly allows a set of known-good, safe inputs. Everything else is rejected.
* Example: For a username, you might only allow alphanumeric characters and a hyphen. If input is "john-doe", it passes. If it is "<script>", it is rejected.

> Purpose:

* To reduce the attack surface by allowing only verified or legitimate sources.

* Prevent unauthorized access or execution.

> Advantages:

* High security (default deny).

* Prevents zero-day attacks (if not on allow list, it can’t run).

* Easy to monitor trusted activity.

> Disadvantages:

*  Harder to manage in dynamic environments.

 *Can block legitimate traffic if not updated.


> Purpose:

 * To stop known bad actors or patterns of malicious behavior.

> Advantages:

* Easier to implement and manage.

* Suitable for open systems needing wide access.

> Disadvantages:

* Less secure (default allow).

* Ineffective against new/unknown threats (zero-days).

* Requires constant updates.

- Block List (Blacklisting): This is insecure and unreliable. It tries to block a list of known-bad inputs
  (e.g., rejecting "<script>", "DROP TABLE"). Attackers can often bypass block lists by using different encoding, capitalization, or by finding a new attack string you didn't include. 

> Levels of input validation:

* Syntactic validation: This checks if the data has the correct format and structure. You can use this to check things like:

* Data type: Is the input a number when it's supposed to be?

* Length: Is the input shorter than the maximum length?

* Regular expressions: Does the input for a phone number match the format (XXX) XXX-XXXX?

* Semantic validation: This checks if the data makes logical sense within the context of your application.

* Example: A user's account creation form asks for a start and end date. Semantic validation would check that the end date is not before the start date. 

* Validation for specific attack types: 

1. Preventing injection: To stop attacks like SQL Injection, use parameterized queries or prepared statements. This is the only safe method, as it separates the user's input from the database command.

2. Preventing Cross-Site Scripting (XSS): Before displaying user-supplied input back to a web page, you must encode the output. This turns special characters like < and > into their harmless encoded versions (&lt; and &gt;), so the browser displays them as text instead of executing them as code.

3. Securing file uploads: This is a high-risk area.

4. Check file type: Validate the file's content type, not just its extension, which is easy to spoof.

5. Limit size: Restrict the maximum file size to prevent denial-of-service attacks.

6. Scan for malware: Use an antivirus scanner on uploaded files.

7. Rename files: Rename uploaded files with a randomly generated name (e.g., a UUID) to prevent attackers from predicting and executing their uploaded script.



