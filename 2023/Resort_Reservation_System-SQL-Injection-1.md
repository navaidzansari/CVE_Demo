# Resort Reservation System - SQL Injection on page view_room.php and parameter is id, application url is (?page=view_room&id=4) with low privilege authentication

### Date: 
> 26 April 2023

### CVE Assigned:
Pending

### Author Name: 
> Muhammad Navaid Zafar Ansari
### Author Email: 
> navaidnasari@hotmail.co.uk
### Vendor Homepage:
> https://www.sourcecodester.com
### Software Link:
> [Resort Reservation System](https://www.sourcecodester.com/php/16447/resort-reservation-system-php-and-sqlite3-source-code-free-download.html)
### Version:
> v 1.0
### SQL Injection
> SQL Injection is a type of vulnerability in web applications that allows an attacker to execute unauthorized SQL queries on the database by exploiting the application's failure to properly validate user input. The attacker can use this vulnerability to bypass the security measures put in place by the application, allowing them to access or modify sensitive data, or even take control of the entire system. SQL Injection attacks can have severe consequences, including data loss, financial loss, reputational damage, and legal liability. To prevent SQL Injection attacks, developers should properly sanitize and validate all user input, and implement strong security measures, such as input validation, output encoding, parameterized queries, and access controls. Users should also be aware of the risks of SQL Injection attacks and take appropriate measures to protect their data.
### Affected Page:
> view_room.php

> On this page id parameter is vulnerable to SQL Injection Attack

> URL of the vulnerable parameter is: ?page=view_room&id=*
### Description:
> The Resort Reservation System supports two roles of users, one is admin, and another is a normal employee. the detail of role is given below
+ Admin user has full access to the system 
+ Employee user has only a few menu access
> Employee could perform the SQL Injection by viewing the room list from his/her profile. Therefore, low-privileged users could able to get the access full system.
### Proof of Concept:
> Following steps are involved:
+ An employee view the room list and could perform the SQL injection with vulnerable parameter (?page=view_room&id=*)
### Request:
```
GET /php-sqlite-rrs/?page=view_room&id=7 HTTP/1.1
Host: localhost
sec-ch-ua: "Not:A-Brand";v="99", "Chromium";v="112"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Linux"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.5615.138 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost/php-sqlite-rrs/?page=rooms&from=2023-03-26&to=2023-04-26
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: PHPSESSID=d723dc8984528029f975c705200f3499
Connection: close
```

### Response:
![image](https://user-images.githubusercontent.com/123810418/234538291-b86d036a-4fe9-4d14-9059-6a113358ffad.png)


### Recommendation:
> Whoever uses this CMS, should update the code of the application in to parameterized queries to avoid SQL Injection attack:
> vulnerable line in 
```
Example Code: 
$sql = $conn->db->prepare("SELECT * FROM `room_list` where `room_id` = :id ");
$sql->bindparam(':id', $_GET['id']);
$sql->execute();
$row = $sql->fetch(PDO::FETCH_ASSOC);
```
Thank you for reading
