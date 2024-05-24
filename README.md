# WAFRules-Attacks

### Lista de Ataques e Regras WAF com Regex

#### 1. Arbitrary File Access
**Ataque**:
- Acesso arbitrário a arquivos.

**Regex**:
```regex
(page=|file=).*(\.\./|\.\.\\)
```

**Regras WAF**:
```apache
SecRule ARGS "(page=|file=).*(\.\./|\.\.\\)" "id:1001,deny,status:403,msg:'Arbitrary File Access attempt detected'"
```

#### 2. Binary Planting
**Ataque**:
- Plantação de binários maliciosos.

**Regex**:
```regex
\.exe$|\.dll$|\.bat$
```

**Regras WAF**:
```apache
SecRule FILES_TMPNAMES "\.exe$|\.dll$|\.bat$" "id:1002,deny,status:403,msg:'Binary Planting attempt detected'"
```

#### 3. Blind SQL Injection
**Ataque**:
- SQL Injection cega.

**Regex**:
```regex
\bAND\b.*\bSLEEP\b|\bWAITFOR\b
```

**Regras WAF**:
```apache
SecRule ARGS "\bAND\b.*\bSLEEP\b|\bWAITFOR\b" "id:1003,deny,status:403,msg:'Blind SQL Injection attempt detected'"
```

#### 4. Blind XPath Injection
**Ataque**:
- XPath Injection cega.

**Regex**:
```regex
xpath\(
```

**Regras WAF**:
```apache
SecRule ARGS "xpath\(" "id:1004,deny,status:403,msg:'Blind XPath Injection attempt detected'"
```

#### 5. Brute Force Attack
**Ataque**:
- Ataque de força bruta.

**Regex**:
```regex
/login.*(username|password)
```

**Regras WAF**:
```apache
SecRule REQUEST_URI "/login.*(username|password)" "id:1005,chain,deny,status:403,msg:'Brute Force attempt detected'"
SecRule REQUEST_HEADERS:Authorization "^(Basic|Digest) [A-Za-z0-9=+/]+$"
```

#### 6. Buffer Overflow Attack
**Ataque**:
- Buffer Overflow.

**Regex**:
```regex
.{1024,}
```

**Regras WAF**:
```apache
SecRule ARGS ".{1024,}" "id:1006,deny,status:403,msg:'Buffer Overflow attempt detected'"
```

#### 7. Cache Poisoning
**Ataque**:
- Envenenamento de cache.

**Regex**:
```regex
X-Forwarded-Host|X-Forwarded-For|X-Forwarded-Scheme
```

**Regras WAF**:
```apache
SecRule REQUEST_HEADERS "X-Forwarded-Host|X-Forwarded-For|X-Forwarded-Scheme" "id:1007,deny,status:403,msg:'Cache Poisoning attempt detected'"
```

#### 8. Clickjacking
**Ataque**:
- Clickjacking.

**Regex**:
```regex
<iframe
```

**Regras WAF**:
```apache
SecRule RESPONSE_BODY "<iframe" "id:1008,deny,status:403,msg:'Clickjacking attempt detected'"
Header always append X-Frame-Options DENY
```

#### 9. Command Injection
**Ataque**:
- Injeção de comandos.

**Regex**:
```regex
(\b(ls|cat|rm|nc|wget|curl)\b)|(\||&|;|`|\$\(.*\))
```

**Regras WAF**:
```apache
SecRule ARGS "(\b(ls|cat|rm|nc|wget|curl)\b)|(\||&|;|`|\$\(.*\))" "id:1009,deny,status:403,msg:'Command Injection attempt detected'"
```

#### 10. Comment Injection Attack
**Ataque**:
- Injeção de comentários.

**Regex**:
```regex
;--|#|\/\*
```

**Regras WAF**:
```apache
SecRule ARGS ";--|#|\/\*" "id:1010,deny,status:403,msg:'Comment Injection attempt detected'"
```

#### 11. Content Spoofing
**Ataque**:
- Falsificação de conteúdo.

**Regex**:
```regex
fake content|spoofed content
```

**Regras WAF**:
```apache
SecRule RESPONSE_BODY "fake content|spoofed content" "id:1011,deny,status:403,msg:'Content Spoofing attempt detected'"
```

#### 12. Credential Stuffing
**Ataque**:
- Uso de listas de credenciais vazadas.

**Regex**:
```regex
/login.*(username|password)
```

**Regras WAF**:
```apache
SecRule REQUEST_URI "/login.*(username|password)" "id:1012,chain,deny,status:403,msg:'Credential Stuffing attempt detected'"
SecRule REQUEST_HEADERS:Authorization "^(Basic|Digest) [A-Za-z0-9=+/]+$"
```

#### 13. Cross Frame Scripting
**Ataque**:
- Scripting cruzado em frames.

**Regex**:
```regex
<iframe
```

**Regras WAF**:
```apache
SecRule RESPONSE_BODY "<iframe" "id:1013,deny,status:403,msg:'Cross Frame Scripting attempt detected'"
Header always append X-Frame-Options DENY
```

#### 14. Cross Site History Manipulation (XSHM)
**Ataque**:
- Manipulação de histórico do site.

**Regex**:
```regex
history\.pushState|history\.replaceState
```

**Regras WAF**:
```apache
SecRule RESPONSE_BODY "history\.pushState|history\.replaceState" "id:1014,deny,status:403,msg:'Cross Site History Manipulation attempt detected'"
```

#### 15. Cross Site Tracing
**Ataque**:
- Uso do método TRACE.

**Regex**:
```regex
TRACE
```

**Regras WAF**:
```apache
SecRule REQUEST_METHOD "TRACE" "id:1015,deny,status:403,msg:'Cross Site Tracing attempt detected'"
```

#### 16. Cross-Site Request Forgery (CSRF)
**Ataque**:
- Forjamento de requisições entre sites.

**Regex**:
```regex
^(Referer:)(?!.*example\.com)
```

**Regras WAF**:
```apache
SecRule REQUEST_HEADERS:Referer "^(Referer:)(?!.*example\.com)" "id:1016,deny,status:403,msg:'CSRF attempt detected'"
```

#### 17. Cross Site Port Attack (XSPA)
**Ataque**:
- Ataque de porta cruzada.

**Regex**:
```regex
:url=.*\:\/\/
```

**Regras WAF**:
```apache
SecRule ARGS:url ":url=.*\:\/\/" "id:1017,deny,status:403,msg:'Cross Site Port Attack attempt detected'"
```

#### 18. Cross-Site Scripting (XSS)
**Ataque**:
- Scripting entre sites.

**Regex**:
```regex
<script>|onerror|onload|onmouseover
```

**Regras WAF**:
```apache
SecRule ARGS "<script>|onerror|onload|onmouseover" "id:1018,deny,status:403,msg:'XSS attempt detected'"
```

#### 19. Cross-User Defacement
**Ataque**:
- Desfiguração entre usuários.

**Regex**:
```regex
modify|deface
```

**Regras WAF**:
```apache
SecRule ARGS "modify|deface" "id:1019,deny,status:403,msg:'Cross-User Defacement attempt detected'"
```

#### 20. Custom Special Character Injection
**Ataque**:
- Injeção de caracteres especiais.

**Regex**:
```regex
%00|%0d%0a|%0a|%0d
```

**Regras WAF**:
```apache
SecRule ARGS "%00|%0d%0a|%0a|%0d" "id:1020,deny,status:403,msg:'Custom Special Character Injection attempt detected'"
```

#### 21. Denial of Service
**Ataque**:
- Negação de serviço.

**Regex**:
```regex
Content-Length:.*\d{7,}
```

**Regras WAF**:
```apache
SecRule REQUEST_HEADERS:Content-Length "Content-Length:.*\d{7,}" "id:1021,deny,status:403,msg:'DoS attempt detected'"
```

#### 22. Direct Dynamic Code Evaluation (Eval Injection)
**Ataque**:
- Injeção de avaliação de código.

**Regex**:
```regex
eval\(
```

**Regras WAF**:
```apache
SecRule ARGS "eval\(" "id:1022,deny,status:403,msg:'Eval Injection attempt detected'"
```

#### 23. Execution After Redirect (EAR)
**Ataque**:
- Execução após redirecionamento.

**Regex**:
```regex
Location:.*\r\n\r\n
```

**Regras WAF**:
```apache
SecRule RESPONSE_HEADERS:Location "Location:.*\r\n\r\n" "id:1023,deny,status:403,msg:'

Execution After Redirect attempt detected'"
```

#### 24. Exploitation of CORS
**Ataque**:
- Exploração de CORS.

**Regex**:
```regex
Origin:.*(null|file:\/\/|localhost)
```

**Regras WAF**:
```apache
SecRule REQUEST_HEADERS:Origin "Origin:.*(null|file:\/\/|localhost)" "id:1024,deny,status:403,msg:'CORS Exploitation attempt detected'"
```

#### 25. Forced Browsing
**Ataque**:
- Navegação forçada.

**Regex**:
```regex
/admin|/config|/backup
```

**Regras WAF**:
```apache
SecRule REQUEST_URI "/admin|/config|/backup" "id:1025,deny,status:403,msg:'Forced Browsing attempt detected'"
```

#### 26. Form Action Hijacking
**Ataque**:
- Sequestro de ação de formulário.

**Regex**:
```regex
<form.*action=.*http:\/\/
```

**Regras WAF**:
```apache
SecRule RESPONSE_BODY "<form.*action=.*http:\/\/" "id:1026,deny,status:403,msg:'Form Action Hijacking attempt detected'"
```

#### 27. Format String Attack
**Ataque**:
- Injeção de string de formato.

**Regex**:
```regex
%s|%x|%n
```

**Regras WAF**:
```apache
SecRule ARGS "%s|%x|%n" "id:1027,deny,status:403,msg:'Format String Attack attempt detected'"
```

#### 28. Full Path Disclosure
**Ataque**:
- Divulgação completa de caminho.

**Regex**:
```regex
(\/var\/www|C:\\inetpub)
```

**Regras WAF**:
```apache
SecRule RESPONSE_BODY "(\/var\/www|C:\\inetpub)" "id:1028,deny,status:403,msg:'Full Path Disclosure attempt detected'"
```

#### 29. Function Injection
**Ataque**:
- Injeção de função.

**Regex**:
```regex
function\(
```

**Regras WAF**:
```apache
SecRule ARGS "function\(" "id:1029,deny,status:403,msg:'Function Injection attempt detected'"
```

#### 30. Host Header Injection
**Ataque**:
- Injeção de cabeçalho de host.

**Regex**:
```regex
Host:.*\r\n\r\n
```

**Regras WAF**:
```apache
SecRule REQUEST_HEADERS:Host "Host:.*\r\n\r\n" "id:1030,deny,status:403,msg:'Host Header Injection attempt detected'"
```

#### 31. HTTP Response Splitting
**Ataque**:
- Divisão de resposta HTTP.

**Regex**:
```regex
(\%0d\%0a|\%0d|\%0a)
```

**Regras WAF**:
```apache
SecRule REQUEST_HEADERS "(\%0d\%0a|\%0d|\%0a)" "id:1031,deny,status:403,msg:'HTTP Response Splitting attempt detected'"
```

#### 32. HTTP Verb Tampering
**Ataque**:
- Manipulação de verbo HTTP.

**Regex**:
```regex
OPTIONS|TRACE
```

**Regras WAF**:
```apache
SecRule REQUEST_METHOD "OPTIONS|TRACE" "id:1032,deny,status:403,msg:'HTTP Verb Tampering attempt detected'"
```

#### 33. HTML Injection
**Ataque**:
- Injeção de HTML.

**Regex**:
```regex
<.*html.*>
```

**Regras WAF**:
```apache
SecRule ARGS "<.*html.*>" "id:1033,deny,status:403,msg:'HTML Injection attempt detected'"
```

#### 34. LDAP Injection
**Ataque**:
- Injeção LDAP.

**Regex**:
```regex
(\b(|&|\!)\b)
```

**Regras WAF**:
```apache
SecRule ARGS "(\b(|&|\!)\b)" "id:1034,deny,status:403,msg:'LDAP Injection attempt detected'"
```

#### 35. Log Injection
**Ataque**:
- Injeção de logs.

**Regex**:
```regex
(\r|\n)
```

**Regras WAF**:
```apache
SecRule ARGS "(\r|\n)" "id:1035,deny,status:403,msg:'Log Injection attempt detected'"
```

#### 36. Man-in-the-browser Attack
**Ataque**:
- Ataque do homem no navegador.

**Regex**:
```regex
User-Agent
```

**Regras WAF**:
```apache
SecRule REQUEST_HEADERS "User-Agent" "id:1036,deny,status:403,msg:'Man-in-the-browser attempt detected'"
```

#### 37. Man-in-the-middle Attack
**Ataque**:
- Ataque do homem no meio.

**Regex**:
```regex
User-Agent
```

**Regras WAF**:
```apache
SecRule REQUEST_HEADERS "User-Agent" "id:1037,deny,status:403,msg:'Man-in-the-middle attempt detected'"
```

#### 38. One-Click Attack
**Ataque**:
- Ataque de um clique.

**Regex**:
```regex
<iframe.*src=
```

**Regras WAF**:
```apache
SecRule RESPONSE_BODY "<iframe.*src=" "id:1038,deny,status:403,msg:'One-Click Attack attempt detected'"
```

#### 39. Parameter Delimiter
**Ataque**:
- Delimitador de parâmetros.

**Regex**:
```regex
(;|&|%26|%3B)
```

**Regras WAF**:
```apache
SecRule ARGS "(;|&|%26|%3B)" "id:1039,deny,status:403,msg:'Parameter Delimiter attempt detected'"
```

#### 40. Page Takeover
**Ataque**:
- Tomada de página.

**Regex**:
```regex
<script>|onerror|onload|onmouseover
```

**Regras WAF**:
```apache
SecRule ARGS "<script>|onerror|onload|onmouseover" "id:1040,deny,status:403,msg:'Page Takeover attempt detected'"
```

#### 41. Path Traversal
**Ataque**:
- Traversal de caminho.

**Regex**:
```regex
(\.\./|\.\.\\)
```

**Regras WAF**:
```apache
SecRule REQUEST_URI "(\.\./|\.\.\\)" "id:1041,deny,status:403,msg:'Path Traversal attempt detected'"
```

#### 42. Reflected DOM Injection
**Ataque**:
- Injeção de DOM refletido.

**Regex**:
```regex
document\.write|document\.cookie|document\.location
```

**Regras WAF**:
```apache
SecRule RESPONSE_BODY "document\.write|document\.cookie|document\.location" "id:1042,deny,status:403,msg:'Reflected DOM Injection attempt detected'"
```

#### 43. Regular expression Denial of Service (ReDoS)
**Ataque**:
- Negação de serviço por expressão regular.

**Regex**:
```regex
(a+)+
```

**Regras WAF**:
```apache
SecRule ARGS "(a+)+" "id:1043,deny,status:403,msg:'ReDoS attempt detected'"
```

#### 44. Repudiation Attack
**Ataque**:
- Ataque de repudiação.

**Regex**:
```regex
action=.*delete
```

**Regras WAF**:
```apache
SecRule ARGS "action=.*delete" "id:1044,deny,status:403,msg:'Repudiation Attack attempt detected'"
```

#### 45. Resource Injection
**Ataque**:
- Injeção de recurso.

**Regex**:
```regex
src=|href=
```

**Regras WAF**:
```apache
SecRule ARGS "src=|href=" "id:1045,deny,status:403,msg:'Resource Injection attempt detected'"
```

#### 46. Server-Side Includes (SSI) Injection
**Ataque**:
- Injeção SSI.

**Regex**:
```regex
<!--#exec
```

**Regras WAF**:
```apache
SecRule ARGS "<!--#exec" "id:1046,deny,status:403,msg:'SSI Injection attempt detected'"
```

#### 47. Session Fixation
**Ataque**:
- Fixação de sessão.

**Regex**:
```regex
(sessionid=|sid=)
```

**Regras WAF**:
```apache
SecRule ARGS "(sessionid=|sid=)" "id:1047,deny,status:403,msg:'Session Fixation attempt detected'"
```

#### 48. Session Hijacking Attack
**Ataque**:
- Sequestro de sessão.

**Regex**:
```regex
(sessionid=|sid=)
```

**Regras WAF**:
```apache
SecRule ARGS "(sessionid=|sid=)" "id:1048,deny,status:403,msg:'Session Hijacking attempt detected'"
```

#### 49. Session Prediction
**Ataque**:
- Previsão de sessão.

**Regex**:
```regex
(sessionid=|sid=)
```

**Regras WAF**:
```apache


SecRule ARGS "(sessionid=|sid=)" "id:1049,deny,status:403,msg:'Session Prediction attempt detected'"
```

#### 50. Setting Manipulation
**Ataque**:
- Manipulação de configurações.

**Regex**:
```regex
(setting=|config=)
```

**Regras WAF**:
```apache
SecRule ARGS "(setting=|config=)" "id:1050,deny,status:403,msg:'Setting Manipulation attempt detected'"
```

#### 51. Special Element Injection
**Ataque**:
- Injeção de elementos especiais.

**Regex**:
```regex
<.*>|&.*;
```

**Regras WAF**:
```apache
SecRule ARGS "<.*>|&.*;" "id:1051,deny,status:403,msg:'Special Element Injection attempt detected'"
```

#### 52. SMTP Injection
**Ataque**:
- Injeção SMTP.

**Regex**:
```regex
(mail=|recipient=|from=|to=)
```

**Regras WAF**:
```apache
SecRule ARGS "(mail=|recipient=|from=|to=)" "id:1052,deny,status:403,msg:'SMTP Injection attempt detected'"
```

#### 53. SQL Injection
**Ataque**:
- Injeção SQL.

**Regex**:
```regex
(\bSELECT\b|\bUNION\b|\bINSERT\b|\bUPDATE\b|\bDELETE\b|\bDROP\b)
```

**Regras WAF**:
```apache
SecRule ARGS "(\bSELECT\b|\bUNION\b|\bINSERT\b|\bUPDATE\b|\bDELETE\b|\bDROP\b)" "id:1053,deny,status:403,msg:'SQL Injection attempt detected'"
```

#### 54. SSI Injection
**Ataque**:
- Injeção SSI.

**Regex**:
```regex
<!--#exec
```

**Regras WAF**:
```apache
SecRule ARGS "<!--#exec" "id:1054,deny,status:403,msg:'SSI Injection attempt detected'"
```

#### 55. Traffic Flood
**Ataque**:
- Enchente de tráfego.

**Regex**:
```regex
GET.*HTTP\/1\.[01]
```

**Regras WAF**:
```apache
SecRule REQUEST_LINE "GET.*HTTP\/1\.[01]" "id:1055,deny,status:403,msg:'Traffic Flood attempt detected'"
```

#### 56. Web Parameter Tampering
**Ataque**:
- Falsificação de parâmetros web.

**Regex**:
```regex
(param=|value=)
```

**Regras WAF**:
```apache
SecRule ARGS "(param=|value=)" "id:1056,deny,status:403,msg:'Web Parameter Tampering attempt detected'"
```

#### 57. XPath Injection
**Ataque**:
- Injeção XPath.

**Regex**:
```regex
xpath\(
```

**Regras WAF**:
```apache
SecRule ARGS "xpath\(" "id:1057,deny,status:403,msg:'XPath Injection attempt detected'"
```

#### 58. XSRF or SSRF
**Ataque**:
- Solicitação forjada entre sites ou solicitação forjada no servidor.

**Regex**:
```regex
(url=|callback=|redir=|continue=)
```

**Regras WAF**:
```apache
SecRule ARGS "(url=|callback=|redir=|continue=)" "id:1058,deny,status:403,msg:'XSRF/SSRF attempt detected'"
```

- **Customização das Regras**: Ajuste as regex conforme necessário para o seu ambiente específico.
- **Monitoramento Contínuo**: Mantenha um monitoramento contínuo para identificar e bloquear novos padrões de ataque.
- **Testes Regulares**: Realize testes periódicos para garantir que as regras estão funcionando corretamente e não estão gerando falsos positivos.
