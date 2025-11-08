# ♥  Certified  ♥  ♥ AppSEc practitioner by-SecOps ♥

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

### Cross-Site Scripting (XSS)
### Definition:

A client-side attack where an attacker injects malicious scripts (usually JavaScript) into web pages viewed by other users.
Goal: Steal cookies, session tokens, or perform actions as the victim.

### How It Works:

Attacker injects malicious code (e.g., <script>alert('Hacked')</script>) into a vulnerable input field.

The server or page reflects it back or stores it without sanitizing.

When another user loads the page, the malicious script executes in their browser.

### Types of XSS
1. Reflected XSS:Payload is reflected off the server immediately
2. DOM-based XSS: Payload is stored in the database or page and served to many users.
3. Stored XSS: Happens entirely in the browser, due to insecure JavaScript manipulation of the DOM.

   <img width="889" height="590" alt="image" src="https://github.com/user-attachments/assets/23ac7060-391c-4398-b6ac-6f1d045d4ca7" />

#### Hashing/Encoding/encryption
♦☺╝          ▐ ☺╤╤♂ •▬ ♣§        !   ♥╒╤○•♦☺♣│╟☺
♦☺╝          ▐ ☺╤╤♂ •▬ ♣§        !   ♥╒╤○•♦☺♣│╟☺
<img width="1230" height="811" alt="image" src="https://github.com/user-attachments/assets/99e279f8-2798-4693-b943-d7944ef674ea" />

#### Encryption :

* An encoding technique, in which a message is encoded by using an encryption algorith in such a way that only authorized personel can access the message or information.
* Special type of encoding for trasfering private data.
* Plain text ◄♦ encryption algorithms like AES or RSa encryption ◄♦ Using a secret key called <ins> CIPHER </ins> .
* THe encrypted data is called <ins> Cipher text </ins>, and finally, the secret key can be used by the intended recipient to convert it back to plain tect.
* There are two tpes of encryption algorithms:
  1) Symmetric ◄♦ Data is encoded and decoded with the help of same key.
  2) Asymmetric ◄♦ Data is encoded and decoded with the help of different keys that is <ins> public or private key </ins>.

#### Encoding :

* Data is transformed from one form to another.
* Main aim is to transform data into a form that is radable by most of the systems or that can be used by any external process.
* It can be used for reducing size of audio and video files.
* Each Audio and video format files have coder - decoder .(codec) program.
* It is used to into appropriate format and then decodes it for playback.

  - E.g : ASC|| , BASE64, UNICODE.

#### Hashing:

* Data is converted to the ahsh using some hashing function, whic can be any number.
* Various hashing algorithms are MD5 and SHA256.
* Data once hashed is non-reversible.
* Hash function is used to map data of arbitory size to data of fixed size.
* The data structure <ins> HASH TABLE </ins> is used for storing data.

##### Authentication RElated Vulnerabilities:
They are flaws in the process of verifying a user's  identity that allow an attacker to bypass security.

##### Common Types of Authentication Vulnerabilities:
      * Brute force           * Paswword storage  * password polciy
    
##### Brute force 
##### defination :
Lack of rate limiting on login attempts allows attackers to repeatedly guess credentials until they succeed. 
> There are several variants, each with distinct behaviors and detection patterns.
##### Variants of brute force:
##### a) Simple burte force:
* attacker guesses the passwords for a single user account by trying all possible combinations.
* Usually automated with tools like
>    * Hydra  * Burp Suite Intruder  * John the Ripper
* Works best when:
* the password police allsow short or weak passwords.
* there are no account lockouts or rare limits.
* Responses are consistent (no Captcha or time delay).
***Mitigation:***
* Rate limiting (e.g., max 5 attempts/minute per user/IP).

* Progressive delays (exponential backoff after each failed attempt).

* CAPTCHA after repeated failures.

* Multi-Factor Authentication (MFA).

#####  B) Password Spraying:
  * Instead of attacking one user with many passwords, the attacker uses a few common passwords accross many accounts.

***Mitigation:***
* Monitor for many failed logins accross multiple accounts from a single IP.
* Require complex or passphrase-style passwords.
* Enforce MFA on all accounts.
* Implement adaptive authentication (flag unusual login velocity).

##### c) Credential Suffing:
* The attacker uses username-password pairs leaked from another breach.
* Works because many users reuse passwords across sites.
 ***Mitigation:***
* Check neew passwords against breach databases.
* Enforce unique passwords for each system.
* Implement MFA.
* Detect repeated failed attempts using known breached passwords.

##### d) Hybrid/dictionary 
* Combines dictionary words with simple mutations (adding numbers or symbols).
***Mitigations:***
  * Block weak/common passwords.
  * Use slow hashing algorithms to make offline brute-forcing impractical.

##### e) Offline Brute Forece:
* happens after a data breach where password hashes are stolen.
* Attacker cracks hashes offline using GPU clusters or cloud rigs.


#####♥ 











