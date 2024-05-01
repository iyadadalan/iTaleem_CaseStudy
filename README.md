# iTaleem_CaseStudy

## Group Members
1. Wan Hamzah Iyad bin Wan Adlan (2115449) - Leader
2. Muhammad bin Abas
3. Muhammad Arif Faisal bin Zahari (2117277)

## Assigned Tasks
1. Muhammad bin Abas
2. Wan Hamzah Iyad bin Wan Adlan
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

### <a name="serv"/>e. Content Security Policy (CSP)
#### Identify:
- CSP Header Not Set
  - CWE ID: 693
  - Risk Level: Medium
  - Confidence Level: High
  - The vulnerability is located at <a>https://italeemc.iium.edu.my/</a>
#### Evaluate:
#### Prevent:

### <a name="serv"/>f. JS Library
#### Identify:
- Vulnerable JS Library 
  - CWE ID: 829
  - Risk Level: Medium
  - Confidence Level: Medium
  - The vulnerability is located at https://italeemc.iium.edu.my/lib/requirejs.php/1709768810/core/first.js
#### Evaluate:
#### Prevent:

### <a name="serv"/>g. HTTPS Implementation
#### Identify:
- Strict-Transport-Security Header Not Set
  - CWE ID: 319
  - Risk Level: Medium
  - Confidence Level: High
  - The vulnerability is located at https://italeemc.iium.edu.my/course/view.php?id=14106
#### Evaluate:
#### Prevent:

### <a name="serv"/>h. Cookie Poisoning
#### Identify:
- Timestamp Disclosure - Unix <br>
    - CWE ID: 200 - Exposure of Sensitive Information to an Unauthorized Actor
    - Risk level: Low
    - Confidence level: Low
    - The vulnerability is located at https://italeemc.iium.edu.my/
      
- Information Disclosure - Sensitive Information in URL
    - CWE ID: 200 - Exposure of Sensitive Information to an Unauthorized Actor
    - Risk level: Informational 
    - Confidence level: Medium
- Information Disclosure - Suspicious Comments
    - CWE ID: 200 - Exposure of Sensitive Information to an Unauthorized Actor
    - Risk level: Informational 
    - Confidence level: Low

#### Evaluate:

