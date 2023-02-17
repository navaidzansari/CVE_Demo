# Simple Food Ordering System - Authenticated Reflected Cross Site Scripting

### Date: 
> 17 February 2023

### Author Email: 
> navaidnasari@hotmail.co.uk

### Vendor Homepage:
> https://www.sourcecodester.com

### Software Link:
> [Simple Food Ordering System](https://www.sourcecodester.com/php/15418/simple-food-ordering-system-client-side-phpmysqli-free-source-code.html)

### Version:
> v 1.0

### Affected Page: 
> process_order.php
> In this page order parameter are vulnerable to Reflected Cross Site Scripting Attack

### Risk:
> Reflected cross-site scripting (XSS) is a type of web vulnerability that occurs when a web application fails to properly sanitize user input, allowing an attacker to inject malicious code into the application's response to a user's request. When the user's browser receives the response, the malicious code is executed, potentially allowing the attacker to steal sensitive information or take control of the user's account.

### Proof of Concept:
> Initially, I tired to verify the XSS attack, I have used normal XSS payload `<script>alert("Verification");</script>` and Below Image confirmed that, the parameter is vulnerable to relfected xss.
> ![image](https://user-images.githubusercontent.com/123810418/219716828-62b529c9-8366-4051-8b2c-f9065b158089.png)

> Based on that, I have decided to make it realistic attack and use burp colloborator to hijack user cookie:
>  ![image](https://user-images.githubusercontent.com/123810418/219717379-d085a7ec-29d4-4d2c-ba19-69e5011891e8.png)

### Recommendation: 
> Whoever uses this CMS, should update line no 41 of process_order.php with the following code to avoid cross-site scripting attack:
```
Old Code: <?php echo $_GET['order']; ?>
New Code: <?php echo htmlspecialchars(strip_tags($_GET['order'])); ?>
```

Thank you for reading
