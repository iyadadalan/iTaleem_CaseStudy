# iTaleem_CaseStudy

## Group Members
1. Wan Hamzah Iyad bin Wan Adlan (2115449) - Leader
2. Muhammad bin Abas
3. Muhammad Arif Faisal bin Zahari (2117277)

## Assigned Tasks
1. Muhammad bin Abas
    - Identify, evaluate and prevent of:
      - Hash Disclosure.
      - CSRF. 
      - Secured Cookies.

3. Wan Hamzah Iyad bin Wan Adlan
    - Identify, evaluate and prevent of:
      - CSP
      - JS Library
      - HTTPS implementation (TLS/SSL)

4. Muhammad Arif Faisal bin Zahari (2117277)
    - Identify, evaluate and prevent of:
      - Cookie Poisoning
      - Potential XSS
      - Information Disclosure


## <a name="obsv"/>Observation Results

### <a name="serv"/>a. Server OS and Server Side-Scripting
#### Identify:

#### Evaluate:

#### Prevent:



### <a name="hash"/>b. Hash Disclosure
#### Identify:
- No alert was gained from the automated or manual scan. This vulnerability has a low-risk level, and the weakness ID for CWE is 200, which stands for Exposure of Sensitive Information to an Unauthorized Actor <a>https://www.zaproxy.org/docs/alerts/10097/</a>.

#### Evaluate:
- N.A. for this website. This web application has prevented and concealed their hashed form of information.

#### Prevent:
- N.A. for this website. Otherwise, ensure that the web server or database does not leak hashes used to protect credentials or other resources. There is typically no requirement that password hashes be accessible to the web browser.

### <a name="serv"/>c. CSRF
#### Identify:
- Absence of Anti-CSRF Tokens
  - CWE ID: 352 - Cross-Site Request Forgery (CSRF)
  - WASC ID: 9
  - Risk Level: Medium
  - Confidence Level: Low
  - The vulnerability is located at <a>https://italeemc.iium.edu.my/</a>
  - Evidence:<br>
    ![CSRF](https://github.com/iyadadalan/iTaleem_CaseStudy/assets/122088412/2f2225e6-6771-4eb5-a137-37bdf806d82e)
    No known Anti-CSRF token: ```[anticsrf, CSRFToken, __RequestVerificationToken, csrfmiddlewaretoken, authenticity_token, OWASP_CSRFTOKEN, anoncsrf, csrf_token, _csrf, _csrfSecret, __csrf_magic, CSRF, _token, _csrf_token] was found in the following HTML form: [Form 1: "anchor" "logintoken" "password" "rememberusername" "username" ]```

#### Evaluate:
No Anti-CSRF tokens were found in a HTML submission form.

A cross-site request forgery is an attack that involves forcing a victim to send an HTTP request to a target destination without their knowledge or intent in order to perform an action as the victim. The underlying cause is application functionality using predictable URL/form actions in a repeatable way. The nature of the attack is that CSRF exploits the trust that a web site has for a user. By contrast, cross-site scripting (XSS) exploits the trust that a user has for a web site. Like XSS, CSRF attacks are not necessarily cross-site, but they can be. Cross-site request forgery is also known as CSRF, XSRF, one-click attack, session riding, confused deputy, and sea surf.

CSRF attacks are effective in a number of situations, including:
    * The victim has an active session on the target site.
    * The victim is authenticated via HTTP auth on the target site.
    * The victim is on the same local network as the target site.

CSRF has primarily been used to perform an action against a target site using the victim's privileges, but recent techniques have been discovered to disclose information by gaining access to the response. The risk of information disclosure is dramatically increased when the target site is vulnerable to XSS, because XSS can be used as a platform for CSRF, allowing the attack to operate within the bounds of the same-origin policy.
![Observed Examples](https://github.com/iyadadalan/iTaleem_CaseStudy/assets/122088412/000acb89-3b49-4920-8a11-1475983fe2df)

Reference: <a>https://cwe.mitre.org/data/definitions/352.html</a>

#### Related:
- OWASP_2021_A01: Broken Access Control - Weaknesses in access control that allow unauthorized access to data or functionality.
- WSTG-v42-SESS-05: Testing for Cross Site Request Forgery - This is a comprehensive resource by the OWASP that provides methodologies and guidance for testing the security of web applications.
- OWASP_2017_A06: Security Misconfiguration - The dangers of inadequate security settings across application stacks or servers that could expose them to attack.

#### Prevent:
- Phase: Architecture and Design
    - Use a vetted library or framework that does not allow this weakness to occur or provides constructs that make this weakness easier to avoid. For example, use anti-CSRF packages such as the OWASP CSRFGuard.
    - Generate a unique nonce for each form, place the nonce into the form, and verify the nonce upon receipt of the form. Be sure that the nonce is not predictable (CWE-330) (Note that this can be bypassed using XSS).
    - Identify especially dangerous operations. When the user performs a dangerous operation, send a separate confirmation request to ensure that the user intended to perform that operation (Note that this can be bypassed using XSS).

- Use the ESAPI Session Management control. This control includes a component for CSRF.

- Do not use the GET method for any request that triggers a state change. For example, if you want to delete a user account, instead of using a simple GET request with a delete confirmation link ``` delete_account.php?confirm=yes```, use a POST request with a hidden form field containing a CSRF token. This enforces a more secure interaction where the user submits data through a form, making it harder for attackers to exploit CSRF vulnerabilities.

- Phase: Implementation
    - Ensure that your application is free of cross-site scripting issues, because most CSRF defenses can be bypassed using attacker-controlled script.
    - Check the HTTP Referer header to see if the request originated from an expected page. This could break legitimate functionality, because users or proxies may have disabled sending the Referer for privacy reasons.

Reference: <a>https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html</a>

### <a name="serv"/>d. Secured Cookies
#### Identify:
- Cookie No HttpOnly Flag
    - CWE ID: 1004 - Sensitive Cookie Without 'HttpOnly' Flag
    - WASC ID: 13
    - Risk Level: Low
    - Confidence Level: Medium
    - The vulnerability is located at <a>https://italeemc.iium.edu.my/</a>
    - Evidence:<br>
          ![moodleSession](https://github.com/iyadadalan/iTaleem_CaseStudy/assets/122088412/11fc25d8-21fb-41e7-861e-33a9ecac50d5)
          
#### Evaluate:
The product uses a cookie to store sensitive information, but the cookie is not marked with the HttpOnly flag.

The HttpOnly flag directs compatible browsers to prevent client-side script from accessing cookies. Including the HttpOnly flag in the Set-Cookie HTTP response header helps mitigate the risk associated with Cross-Site Scripting (XSS) where an attacker's script code might attempt to read the contents of a cookie and exfiltrate information obtained. When set, browsers that support the flag will not reveal the contents of the cookie to a third party via client-side script executed via XSS.

A cookie has been set without the HttpOnly flag, which means that the cookie can be accessed by JavaScript. If a malicious script can be run on this page then the cookie will be accessible and can be transmitted to another site. If this is a session cookie then session hijacking may be possible.

Reference: <a>https://cwe.mitre.org/data/definitions/1004.html</a>

#### Related:
- OWASP_2021_A01: Broken Access Control - Weaknesses in access control that allow unauthorized access to data or functionality.
- WSTG-v42-SESS-05: Testing for Cross Site Request Forgery - This is a comprehensive resource by the OWASP that provides methodologies and guidance for testing the security of web applications.
- OWASP_2017_A06: Security Misconfiguration - The dangers of inadequate security settings across application stacks or servers that could expose them to attack.

#### Prevent:
Ensure that the HttpOnly flag is set for all cookies. While this mitigation is effective for protecting cookies from a browser's own scripting engine, third-party components or plugins may have their own engines that allow access to cookies. Attackers might also be able to use XMLHTTPResponse to read the headers directly and obtain the cookie.

### <a name="serv"/>e. Content Security Policy (CSP)
#### Identify:
- CSP Header Not Set
  - CWE ID: 693 - Protection Mechanism Failure
  - Risk Level: Medium
  - Confidence Level: High
  - The vulnerability is located at <a>https://italeemc.iium.edu.my/</a>
  - Evidence:<br>
    ![image](images/CSP.png)
#### Evaluate:
Content Security Policy (CSP) is an added layer of security that helps to detect and mitigate certain types of attacks, including Cross Site Scripting (XSS) and data injection attacks. These attacks are used for everything from data theft to site defacement or distribution of malware. CSP provides a set of standard HTTP headers that allow website owners to declare approved sources of content that browsers should be allowed to load on that page — covered types are JavaScript, CSS, HTML frames, fonts, images and embeddable objects such as Java applets, ActiveX, audio and video files.

In this case, the meta tag in the code for this page does not include a Content Security Policy in the ```meta``` tag. Adding a CSP can significantly enhance the site’s security by restricting resource loading to trusted sources and reducing the risk of XSS attacks. 

#### Related:
- OWASP_2021_A05: Security Misconfiguration - the risk and prevalence of security weaknesses caused by incorrect security settings in applications and servers.
- OWASP_2017_A06: Security Misconfiguration - the dangers of inadequate security settings across application stacks or servers that could expose them to attack.

#### Prevent:
Ensure that your web server, application server, load balancer, etc. is configured to set the Content-Security-Policy header. For example:<br>
```<meta http-equiv="Content-Security-Policy" content="default-src 'self'; img-src 'self' https://*.iium.edu.my; script-src 'self' https://italeemc.iium.edu.my; style-src 'self' https://italeemc.iium.edu.my;">```

### <a name="serv"/>f. JS Library
#### Identify:
- Vulnerable JS Library
  - CWE ID: 829 - Inclusion of Functionality from Untrusted Control Sphere
  - Risk Level: Medium
  - Confidence Level: Medium
  - The vulnerability is located at https://italeemc.iium.edu.my/lib/requirejs.php/1709768810/core/first.js
  - Evidence: ```t.data("selectpicker",o=new p(this,r))}"string"==typeof s&&(i=o[s]instanceof Function?o[s].apply(o,n):o.options[s])}});return void 0!==i?i:o}p.VERSION="1.12.4"```
#### Evaluate:

A JavaScript library threat in web security refers to the vulnerabilities that can arise from using third-party JavaScript libraries in web applications.  These libraries, while essential for developing interactive and efficient websites, can introduce various security risks if not properly managed or updated. Common threats such as Cross-Site Scripting (XSS) and SQL injections will take advantage of this exposure.

In this case, the version ```1.12.4``` of the ```bootstrap-select``` library has a security issue. It's vulnerable to Cross-Site Scripting (XSS) because it doesn't properly handle special characters in the titles of dropdown options. This may allow attackers to execute unwanted JavaScript code in a victim's browser.

Related:
- CVE-2019-20921: bootstrap-select before 1.13.6 allows Cross-Site Scripting (XSS). It does not escape title values in OPTION elements. This may allow attackers to execute arbitrary JavaScript in a victim's browser.
- OWASP_2017_A09: Using Components with Known Vulnerabilities - the dangers of using software components that are out-of-date or have publicly disclosed vulnerabilities.
- OWASP_2021_A06: Vulnerable and Outdated Components - using software components that have known vulnerabilities due to being outdated or unmaintained.

#### Prevent:
- Upgrade Components: Upgrading to the latest version of bootstrap-select will usually fix the vulnerabilites of past versions
- Implement Content Security Policies (CSP): CSPs can prevent unauthorisde scripts from running on your website.

#### References:
- https://nvd.nist.gov/vuln/detail/CVE-2019-20921
- https://owasp.org/www-project-top-ten/2017/A9_2017-Using_Components_with_Known_Vulnerabilities
- https://owasp.org/Top10/A06_2021-Vulnerable_and_Outdated_Components/

### <a name="serv"/>g. HTTPS Implementation
#### Identify:
- Strict-Transport-Security Header Not Set
  - CWE ID: 319 - Cleartext Transmission of Sensitive Information
  - Risk Level: Medium
  - Confidence Level: High
  - The vulnerability is located at https://italeemc.iium.edu.my/course/view.php?id=14106
#### Evaluate:
HTTP Strict Transport Security (HSTS) is a web security policy mechanism whereby a web server declares that complying user agents (such as a web browser) are to interact with it using only secure HTTPS connections (i.e. HTTP layered over TLS/SSL). HSTS is an IETF standards track protocol and is specified in RFC 6797.
#### Prevent:

### <a name="serv"/>h. Cookie Poisoning
#### Identify:
There is no alert found by OWASP ZAP for this vulnerability

#### Evaluate:
Not available on this website. Cookie poisoning occurs when attackers manipulate cookies to inject malicious data or modify existing data, potentially compromising the security and integrity of a web application. Attackers may exploit weaknesses in the application's handling of cookies, such as insufficient validation or sanitization of cookie values.

#### Prevent:
- Ensure that cookies are set with secure attributes such as ```HttpOnly```, ```Secure```, and ```SameSite``` to mitigate the risk of cookie poisoning attacks.
- Implement strict validation and sanitization mechanisms to validate user-supplied data before storing it in cookies.
  
### <a name="serv"/>i. Potential XSS
#### Identify:
- X-Content-Type-Options Header Missing
  - CWE ID: 693
#### Evaluate: 
The absence of the X-Content-Type-Options header exposes the application to risks associated with MIME-sniffing attacks. Without this header, some older versions of Internet Explorer and Chrome can perform MIME-sniffing on the response body. It potentially causes the response body to be interpreted and displayed as a content type other than the declared content type. Attackers could exploit this behaviour to execute malicious code or bypass security controls, potentially leading to XSS (Cross-Site Scripting) or other attacks.

#### Prevent:
- Configure web servers or application frameworks to include the X-Content-Type-Options header in HTTP responses. Set the value of this header to "nosniff" to instruct web browsers not to perform MIME-sniffing and instead adhere strictly to the declared content type. <br>
```X-Content-Type-Options: nosniff```
- When serving resources, make sure you send the content-type header to appropriately match the type of the resource being served. For example, if you are serving an HTML page, you should send the HTTP header:<br>
```Content-Type: text/html```
### <a name="serv"/>j. Information Disclosure
#### Identify:
1. Timestamp Disclosure - Unix <br>
    - CWE ID: 200 - Exposure of Sensitive Information to an Unauthorized Actor
    - Risk level: Low
    - Confidence level: Low
    - The vulnerability is located at https://italeemc.iium.edu.my/
    - ```1709768810```, which evaluates to: ```2024-03-07 07:46:50``` <br><br>
      ![image](images/Timestamp.PNG)
#### Evaluate:

The vulnerability of timestamp disclosure in Unix occurs when an application or web server inadvertently reveals the timestamp of a request or response. It presents several significant risks that can compromise the security and integrity of the system. One key risk is information leakage, where attackers can gain insights into the system's activity patterns through exposed timestamps. This information may reveal sensitive details about system operations or user activities, providing attackers with valuable reconnaissance for potential exploits or attacks. Additionally, timestamp disclosure can expand the attack surface of the system by providing attackers with additional information to refine and target their attacks more effectively. Attackers can organise timing-based attacks, such as timing attacks or replay attacks that exploit vulnerabilities or compromise system integrity.

#### Related CVE:
- CVE-1999-0524: The remote host responds to an ICMP timestamp request, which allows an attacker to determine the time and date on your host. This information could potentially help attackers defeat time-based authentication schemes.

#### Prevent:
- Modify the Unix server configuration to prevent the disclosure of timestamps by the application or web server. This can typically be achieved by adjusting the server’s logging settings or by disabling the specific feature that is causing the disclosure.
- Keep the Unix server up to date with the latest security patches and updates. This helps to address any known vulnerabilities, including those related to timestamp disclosure.
- Ensure that appropriate access controls are in place to restrict access to sensitive information, including timestamps. This can involve configuring file permissions, user privileges, and network security measures.
  
2. Information Disclosure - Sensitive Information in URL
    - CWE ID: 200 - Exposure of Sensitive Information to an Unauthorized Actor
    - Risk level: Informational 
    - Confidence level: Medium
    - The vulnerability is located at https://italeemc.iium.edu.my/login/index.php?authCAS=CAS&ticket=ST-1431048-TQy56uUdIzxJp51ANyZ66-mG9h8-cas2
    - Evidence: ```ticket```

#### Evaluate:
The occurrence of "Information Disclosure - Sensitive Information in URL" implies that the HTTP request might contain confidential data leaked through the URL. This could result in unauthorized exposure, violating PCI (Payment Card Industry) standards and many organizational compliance regulations. Consequently, error messages may surface during PCI compliance assessments.

##### Related CVE:
- CVE-2020-7932: In versions of OMERO.web prior to 5.6.3, there is an optional feature that allows certain sensitive data elements, like session keys, to be included as URL query parameters. If an attacker manages to deceive a user into clicking on a malicious link within OMERO.web, the data contained in these query parameters might be revealed in the Referer header observed by the targeted user. Additionally, information present in the URL path, such as object IDs, could also be disclosed.

#### Prevent:
- Compartmentalize the system to have “safe” areas where trust boundaries can be drawn. Do not allow sensitive data to go outside of the trust boundary and always be careful when interfacing with a compartment outside of the safe area.
- Do not pass sensitive information in URIs.

3. Information Disclosure - Suspicious Comments
    - CWE ID: 200 - Exposure of Sensitive Information to an Unauthorized Actor
    - Risk level: Informational 
    - Confidence level: Low
    - The vulnerability is located at https://italeemc.iium.edu.my/lib/javascript.php/1709768810/lib/javascript-static.js
    - Evidence: ```admin```
#### Evaluate:

Exposed comments or sections of source code that have been commented out could assist attackers in comprehending the underlying logic of your application. This information might enable them to identify operational endpoints among other things. By examining these fragments and actual code comments, attackers could uncover flaws in security protocols and discover unused yet accessible endpoints that could potentially expose sensitive data. Additionally, they may gain insights into internal company details, such as developers' personal names or the structure of the internal network.

#### Prevent:
- Eliminate any exposed code comments that could aid attackers and address the underlying issues they indicate.
  
