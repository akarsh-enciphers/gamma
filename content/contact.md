+++
title = "Challenges on Threads"
date = "2020-12-16"
sidemenu = "true"
description = "Developed by Enciphers"
+++

As we know there are many vulnerabilities present in the Threads web application so to find out and exploit each of  these vulnerabilities are the challenges on Threads application. We have categorized the vulnerabilities into 4 parts (low,medium,high,critical) on the basis of how it is going to effec your system.
###### Note: (hint on how to solve the challenge is  provided under the heading of each challenge in a small paragraph, so read them at your own risks).   
Here is the list of all the challenges which a user can solve:

## Low Risk Challenges

### Self XSS

**About**: Reflected attacks are those where the injected script is reflected off the web server, such as in an error message, search result, or any other response that includes some or all of the input sent to the server as part of the request. Reflected attacks are delivered to victims via another route, such as in an e-mail message, or on some other website. When a user is tricked into clicking on a malicious link, submitting a specially crafted form, or even just browsing to a malicious site, the injected code travels to the vulnerable web site, which reflects the attack back to the user’s browser. The browser then executes the code because it came from a “trusted” server.  [Tap to learn more](https://portswigger.net/web-security/cross-site-scripting/reflected) 

**Hint**:  Insert a payload under the name of the account (could be done when registering an account or changing the existing account name for the profile section.


### Hidden Directories

**About**: When a security analyst performing website penetration testing the initial step should be finding hidden directories of a vulnerable website.These hidden web directories are essential because they can give useful information i.e. potential attack vectors that would not be visible on the public facing website.One of the ways to achieve this is by attempting brute-forcing site structure that includes directories and files in websites. 

**Hint**: There is a directory (/management) where we can login as admin with the hardcoded mail which is `test@test.com` . To Brute Force all the directories you can take help of tool Dirsearch. [Click to download the tool](https://github.com/maurosoria/dirsearch)

### Cross-site Request Forgery(CSRF)

**About**: Cross-Site Request Forgery (CSRF) is an attack that forces an end user to execute unwanted actions on a web application in which they’re currently authenticated. With a little help of social engineering (such as sending a link via email or chat), an attacker may trick the users of a web application into executing actions of the attacker’s choosing. If the victim is a normal user, a successful CSRF attack can force the user to perform state changing requests like transferring funds, changing their email address, and so forth. If the victim is an administrative account, CSRF can compromise the entire web application. [Tap to learn more](https://owasp.org/www-community/attacks/csrf)

**Hint**: The Threads application is CSRF vulnerable because it does not create anti csrf tokens. So basically as an attacker you can change victims password, name,other information on profile section. You have to send the malicious link to the victim browser  which should be clicked by  the victim to perform action in it. The malicious file to change victim's password is  attached to the link he sent. 


## Medium Risk Challenges

### MongoDB Injection(NoSQL Injection)

**About**: NoSQL injection vulnerabilities allow attackers to inject code into commands for databases that don’t use SQL queries, such as MongoDB. NoSQL injection attacks can be especially dangerous because code is injected and executed on the server in the language of the web application, potentially allowing arbitrary code execution. [Tap to learn more](https://www.netsparker.com/blog/web-security/what-is-nosql-injection/)

**Hint** : It is present in the search feature of the application where it works like this if the name (exact) matches with the application then it will show that user's id and its information. Also if you pass {$gt: ''}  in the search field, it would show all the users as the query which was executing.


## High RISK Challenges

### Insecure Direct Object Reference

**About**: An insecure direct object reference (IDOR) is an access control vulnerability where unvalidated user input can be used for unauthorized access to resources or operations. IDORs can have serious consequences for cybersecurity and be very hard to find, though exploiting them can be as simple as manually changing a URL parameter. [Click to learn more](https://portswigger.net/web-security/access-control/idor)

**Hint**:  Deleting Comment/Post of any user using BurpSuite (having the UUID).

### Server-side Request Forgery(SSRF)

**About**: In a Server-Side Request Forgery (SSRF) attack, the attacker can abuse functionality on the server to read or update internal resources. The attacker can supply or modify a URL which the code running on the server will read or submit data to, and by carefully selecting the URLs, the attacker may be able to read server configuration such as AWS metadata, connect to internal services like http enabled databases or perform post requests towards internal services which are not intended to be exposed. [Click to learn more](https://owasp.org/www-community/attacks/Server_Side_Request_Forgery)

**Hint**: So it is in  the profile section where you can upload your profile picture via URL, its very simple basics SSRF. You can fetch internal files(which exists) on the server like /etc/passwd .Then inspect the profile page and download the updated image you would see the /etc/passwd content .

### Attribute-XSS(Stored XSS)

**About**: Stored attacks are those where the injected script is permanently stored on the target servers, such as in a database, in a message forum, visitor log, comment field, etc. The victim then retrieves the malicious script from the server when it requests the stored information. [Click to learn more](https://portswigger.net/web-security/cross-site-scripting/stored) 

**Hint**:  Under the profile section, you can change your website link, it would execute only when visited in an unauthenticated state.


## Critical Risk Challenges  

### JWT Authentication

**About**: JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA or ECDSA. [Click to learn more](https://jwt.io/introduction/)

**Note**:  For JWT challenge, hardcoded email is *‘test@test.com’* and the password for it is *‘123’*. So first make sure that an account exists with the above email id and then try to forge the token.

**Hint**:  The application uses cookie-based authentication but has the support of JWT as well.There is a /management page which has an authentication system which works via JWT API. When logging in to the /management page by providing your credentials, you would see that you are not authorized to log in. Now to become authorized user one has to forge the token of the admin account since its using HMAC so the current secret key is thr3@ds@000t so forge a token with *‘test@test.com’*.You can replace the token via burp request and response or just change the token under local storage and refresh the page you should have admin access where you can delete other users.

These are all the challenges present on Threads application which you can solve.
Happy learning,Happy hacking!
 

