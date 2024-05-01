# iTaleem_CaseStudy

## Group Members
1. Muhammad Arif Faisal bin Zahari (2117277)

## Assigned Tasks
1. Muhammad bin Abas
2. Muhammad Arif Faisal bin Zahari (2117277)
    - Identify, evaluate and prevent of:
      - Cookie Poisoning
      - Potential XSS
      - Information Disclosure

## <a name="obsv"/>Observation Results
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

#### Prevent
- Modify the Unix server configuration to prevent the disclosure of timestamps by the application or web server. This can typically be achieved by adjusting the server’s logging settings or by disabling the specific feature that is causing the disclosure.
- Keep the Unix server up to date with the latest security patches and updates. This helps to address any known vulnerabilities, including those related to timestamp disclosure.
- Ensure that appropriate access controls are in place to restrict access to sensitive information, including timestamps. This can involve configuring file permissions, user privileges, and network security measures.
  
2. Information Disclosure - Sensitive Information in URL
    - CWE ID: 200 - Exposure of Sensitive Information to an Unauthorized Actor
    - Risk level: Informational 
    - Confidence level: Medium
    - The vulnerability is located at https://italeemc.iium.edu.my/login/index.php?authCAS=CAS&ticket=ST-1431048-TQy56uUdIzxJp51ANyZ66-mG9h8-cas2
    - Evidence: ```ticket```

#### Evaluate 
The occurrence of "Information Disclosure - Sensitive Information in URL" implies that the HTTP request might contain confidential data leaked through the URL. This could result in unauthorized exposure, violating PCI (Payment Card Industry) standards and many organizational compliance regulations. Consequently, error messages may surface during PCI compliance assessments.

##### Related CVE
- CVE-2020-7932: In versions of OMERO.web prior to 5.6.3, there is an optional feature that allows certain sensitive data elements, like session keys, to be included as URL query parameters. If an attacker manages to deceive a user into clicking on a malicious link within OMERO.web, the data contained in these query parameters might be revealed in the Referer header observed by the targeted user. Additionally, information present in the URL path, such as object IDs, could also be disclosed.

#### Prevent
- Compartmentalize the system to have “safe” areas where trust boundaries can be drawn. Do not allow sensitive data to go outside of the trust boundary and always be careful when interfacing with a compartment outside of the safe area.
- Do not pass sensitive information in URIs.

3. Information Disclosure - Suspicious Comments
    - CWE ID: 200 - Exposure of Sensitive Information to an Unauthorized Actor
    - Risk level: Informational 
    - Confidence level: Low
    - The vulnerability is located at https://italeemc.iium.edu.my/lib/javascript.php/1709768810/lib/javascript-static.js
    - Evidence: ```admin```
#### Evaluate 

Exposed comments or sections of source code that have been commented out could assist attackers in comprehending the underlying logic of your application. This information might enable them to identify operational endpoints among other things. By examining these fragments and actual code comments, attackers could uncover flaws in security protocols and discover unused yet accessible endpoints that could potentially expose sensitive data. Additionally, they may gain insights into internal company details, such as developers' personal names or the structure of the internal network.

#### Prevent
- Eliminate any exposed code comments that could aid attackers and address the underlying issues they indicate.
  
#### Evaluate:

