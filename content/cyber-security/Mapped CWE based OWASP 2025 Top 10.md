---
title: Mapped CWE based OWASP 2025 Top 10
draft: false
tags:
  - owasp top 10
  - cwe
  - cyber security
  - vulnerabilities
---


# A01:2025 - Broken Access Control

1. CWE-22 Improper Limitation of a Pathname to a Restricted Directory ('Path Traversal')

2. CWE-23 Relative Path Traversal

3. CWE-36 Absolute Path Traversal

4. CWE-59 Improper Link Resolution Before File Access ('Link Following')

5. CWE-61 UNIX Symbolic Link (Symlink) Following

6. CWE-65 Windows Hard Link

7. CWE-200 Exposure of Sensitive Information to an Unauthorized Actor

8. CWE-201 Exposure of Sensitive Information Through Sent Data

9. CWE-219 Storage of File with Sensitive Data Under Web Root

10. CWE-276 Incorrect Default Permissions

11. CWE-281 Improper Preservation of Permissions

12. CWE-282 Improper Ownership Management

13. CWE-283 Unverified Ownership

14. CWE-284 Improper Access Control

15. CWE-285 Improper Authorization

16. CWE-352 Cross-Site Request Forgery (CSRF)

17. CWE-359 Exposure of Private Personal Information to an Unauthorized Actor

18. CWE-377 Insecure Temporary File

19. CWE-379 Creation of Temporary File in Directory with Insecure Permissions

20. CWE-402 Transmission of Private Resources into a New Sphere ('Resource Leak')

21. CWE-424 Improper Protection of Alternate Path

22. CWE-425 Direct Request ('Forced Browsing')

23. CWE-441 Unintended Proxy or Intermediary ('Confused Deputy')

24. CWE-497 Exposure of Sensitive System Information to an Unauthorized Control Sphere

25. CWE-538 Insertion of Sensitive Information into Externally-Accessible File or Directory

26. CWE-540 Inclusion of Sensitive Information in Source Code

27. CWE-548 Exposure of Information Through Directory Listing

28. CWE-552 Files or Directories Accessible to External Parties

29. CWE-566 Authorization Bypass Through User-Controlled SQL Primary Key

30. CWE-601 URL Redirection to Untrusted Site ('Open Redirect')

31. CWE-615 Inclusion of Sensitive Information in Source Code Comments

32. CWE-639 Authorization Bypass Through User-Controlled Key

33. CWE-668 Exposure of Resource to Wrong Sphere

34. CWE-732 Incorrect Permission Assignment for Critical Resource

35. CWE-749 Exposed Dangerous Method or Function

36. CWE-862 Missing Authorization

37. CWE-863 Incorrect Authorization

38. CWE-918 Server-Side Request Forgery (SSRF)

39. CWE-922 Insecure Storage of Sensitive Information

40. CWE-1275 Sensitive Cookie with Improper SameSite Attribute

  

# A02:2025 - Security Misconfiguration

1. CWE-5 J2EE Misconfiguration: Data Transmission Without Encryption

2. CWE-11 ASP.NET Misconfiguration: Creating Debug Binary

3. CWE-13 ASP.NET Misconfiguration: Password in Configuration File

4. CWE-15 External Control of System or Configuration Setting

5. CWE-16 Configuration

6. CWE-260 Password in Configuration File

7. CWE-315 Cleartext Storage of Sensitive Information in a Cookie

8. CWE-489 Active Debug Code

9. CWE-526 Exposure of Sensitive Information Through Environmental Variables

10. CWE-547 Use of Hard-coded, Security-relevant Constants

11. CWE-611 Improper Restriction of XML External Entity Reference

12. CWE-614 Sensitive Cookie in HTTPS Session Without 'Secure' Attribute

13. CWE-776 Improper Restriction of Recursive Entity References in DTDs ('XML Entity Expansion')

14. CWE-942 Permissive Cross-domain Policy with Untrusted Domains

15. CWE-1004 Sensitive Cookie Without 'HttpOnly' Flag

16. CWE-1174 ASP.NET Misconfiguration: Improper Model Validation

  

# A03:2025 - Software Supply Chain Failures

1. CWE-447 Use of Obsolete Function

2. CWE-1035 2017 Top 10 A9: Using Components with Known Vulnerabilities

3. CWE-1104 Use of Unmaintained Third Party Components

4. CWE-1329 Reliance on Component That is Not Updateable

5. CWE-1357 Reliance on Insufficiently Trustworthy Component

6. CWE-1395 Dependency on Vulnerable Third-Party Component

  

# A04:2025 - Cryptographic Failures

1. CWE-261 Weak Encoding for Password

2. CWE-296 Improper Following of a Certificate's Chain of Trust

3. CWE-319 Cleartext Transmission of Sensitive Information

4. CWE-320 Key Management Errors (Prohibited)

5. CWE-321 Use of Hard-coded Cryptographic Key

6. CWE-322 Key Exchange without Entity Authentication

7. CWE-323 Reusing a Nonce, Key Pair in Encryption

8. CWE-324 Use of a Key Past its Expiration Date

9. CWE-325 Missing Required Cryptographic Step

10. CWE-326 Inadequate Encryption Strength

11. CWE-327 Use of a Broken or Risky Cryptographic Algorithm

12. CWE-328 Reversible One-Way Hash

13. CWE-329 Not Using a Random IV with CBC Mode

14. CWE-330 Use of Insufficiently Random Values

15. CWE-331 Insufficient Entropy

16. CWE-332 Insufficient Entropy in PRNG

17. CWE-334 Small Space of Random Values

18. CWE-335 Incorrect Usage of Seeds in Pseudo-Random Number Generator(PRNG)

19. CWE-336 Same Seed in Pseudo-Random Number Generator (PRNG)

20. CWE-337 Predictable Seed in Pseudo-Random Number Generator (PRNG)

21. CWE-338 Use of Cryptographically Weak Pseudo-Random Number Generator(PRNG)

22. CWE-340 Generation of Predictable Numbers or Identifiers

23. CWE-342 Predictable Exact Value from Previous Values

24. CWE-347 Improper Verification of Cryptographic Signature

25. CWE-523 Unprotected Transport of Credentials

26. CWE-757 Selection of Less-Secure Algorithm During Negotiation('Algorithm Downgrade')

27. CWE-759 Use of a One-Way Hash without a Salt

28. CWE-760 Use of a One-Way Hash with a Predictable Salt

29. CWE-780 Use of RSA Algorithm without OAEP

30. CWE-916 Use of Password Hash With Insufficient Computational Effort

31. CWE-1240 Use of a Cryptographic Primitive with a Risky Implementation

32. CWE-1241 Use of Predictable Algorithm in Random Number Generator

  

# A05:2025 - Injection

1. CWE-20 Improper Input Validation

2. CWE-74 Improper Neutralization of Special Elements in Output Used by a Downstream Component ('Injection')

3. CWE-76 Improper Neutralization of Equivalent Special Elements

4. CWE-77 Improper Neutralization of Special Elements used in a Command ('Command Injection')

5. CWE-78 Improper Neutralization of Special Elements used in an OS Command ('OS Command Injection')

6. CWE-79 Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')

7. CWE-80 Improper Neutralization of Script-Related HTML Tags in a Web Page (Basic XSS)

8. CWE-83 Improper Neutralization of Script in Attributes in a Web Page

9. CWE-86 Improper Neutralization of Invalid Characters in Identifiers in Web Pages

10. CWE-88 Improper Neutralization of Argument Delimiters in a Command ('Argument Injection')

11. CWE-89 Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection')

12. CWE-90 Improper Neutralization of Special Elements used in an LDAP Query ('LDAP Injection')

13. CWE-91 XML Injection (aka Blind XPath Injection)

14. CWE-93 Improper Neutralization of CRLF Sequences ('CRLF Injection')

15. CWE-94 Improper Control of Generation of Code ('Code Injection')

16. CWE-95 Improper Neutralization of Directives in Dynamically Evaluated Code ('Eval Injection')

17. CWE-96 Improper Neutralization of Directives in Statically Saved Code ('Static Code Injection')

18. CWE-97 Improper Neutralization of Server-Side Includes (SSI) Within a Web Page

19. CWE-98 Improper Control of Filename for Include/Require Statement in PHP Program ('PHP Remote File Inclusion')

20. CWE-99 Improper Control of Resource Identifiers ('Resource Injection')

21. CWE-103 Struts: Incomplete validate() Method Definition

22. CWE-104 Struts: Form Bean Does Not Extend Validation Class

23. CWE-112 Missing XML Validation

24. CWE-113 Improper Neutralization of CRLF Sequences in HTTP Headers ('HTTP Response Splitting')

25. CWE-114 Process Control

26. CWE-115 Misinterpretation of Output

27. CWE-116 Improper Encoding or Escaping of Output

28. CWE-129 Improper Validation of Array Index

29. CWE-159 Improper Handling of Invalid Use of Special Elements

30. CWE-470 Use of Externally-Controlled Input to Select Classes or Code ('Unsafe Reflection')

31. CWE-493 Critical Public Variable Without Final Modifier

32. CWE-500 Public Static Field Not Marked Final

33. CWE-564 SQL Injection: Hibernate

34. CWE-610 Externally Controlled Reference to a Resource in Another Sphere

35. CWE-643 Improper Neutralization of Data within XPath Expressions ('XPath Injection')

36. CWE-644 Improper Neutralization of HTTP Headers for Scripting Syntax

37. CWE-917 Improper Neutralization of Special Elements used in an Expression Language Statement ('Expression Language Injection')

  

# A06:2025 - Insecure Design

1. CWE-73 External Control of File Name or Path

2. CWE-183 Permissive List of Allowed Inputs

3. CWE-256 Unprotected Storage of Credentials

4. CWE-266 Incorrect Privilege Assignment

5. CWE-269 Improper Privilege Management

6. CWE-286 Incorrect User Management

7. CWE-311 Missing Encryption of Sensitive Data

8. CWE-312 Cleartext Storage of Sensitive Information

9. CWE-313 Cleartext Storage in a File or on Disk

10. CWE-316 Cleartext Storage of Sensitive Information in Memory

11. CWE-362 Concurrent Execution using Shared Resource with Improper Synchronization ('Race Condition')

12. CWE-382 J2EE Bad Practices: Use of System.exit()

13. CWE-419 Unprotected Primary Channel

14. CWE-434 Unrestricted Upload of File with Dangerous Type

15. CWE-436 Interpretation Conflict

16. CWE-444 Inconsistent Interpretation of HTTP Requests ('HTTP Request Smuggling')

17. CWE-451 User Interface (UI) Misrepresentation of Critical Information

18. CWE-454 External Initialization of Trusted Variables or Data Stores

19. CWE-472 External Control of Assumed-Immutable Web Parameter

20. CWE-501 Trust Boundary Violation

21. CWE-522 Insufficiently Protected Credentials

22. CWE-525 Use of Web Browser Cache Containing Sensitive Information

23. CWE-539 Use of Persistent Cookies Containing Sensitive Information

24. CWE-598 Use of GET Request Method With Sensitive Query Strings

25. CWE-602 Client-Side Enforcement of Server-Side Security

26. CWE-628 Function Call with Incorrectly Specified Arguments

27. CWE-642 External Control of Critical State Data

28. CWE-646 Reliance on File Name or Extension of Externally-Supplied File

29. CWE-653 Insufficient Compartmentalization

30. CWE-656 Reliance on Security Through Obscurity

31. CWE-657 Violation of Secure Design Principles

32. CWE-676 Use of Potentially Dangerous Function

33. CWE-693 Protection Mechanism Failure

34. CWE-799 Improper Control of Interaction Frequency

35. CWE-807 Reliance on Untrusted Inputs in a Security Decision

36. CWE-841 Improper Enforcement of Behavioral Workflow

37. CWE-1021 Improper Restriction of Rendered UI Layers or Frames

38. CWE-1022 Use of Web Link to Untrusted Target with window.opener Access

39. CWE-1125 Excessive Attack Surface

  

# A07:2025 - Authentication Failures

1. CWE-258 Empty Password in Configuration File

2. CWE-259 Use of Hard-coded Password

3. CWE-287 Improper Authentication

4. CWE-288 Authentication Bypass Using an Alternate Path or Channel

5. CWE-289 Authentication Bypass by Alternate Name

6. CWE-290 Authentication Bypass by Spoofing

7. CWE-291 Reliance on IP Address for Authentication

8. CWE-293 Using Referer Field for Authentication

9. CWE-294 Authentication Bypass by Capture-replay

10. CWE-295 Improper Certificate Validation

11. CWE-297 Improper Validation of Certificate with Host Mismatch

12. CWE-298 Improper Validation of Certificate with Host Mismatch

13. CWE-299 Improper Validation of Certificate with Host Mismatch

14. CWE-300 Channel Accessible by Non-Endpoint

15. CWE-302 Authentication Bypass by Assumed-Immutable Data

16. CWE-303 Incorrect Implementation of Authentication Algorithm

17. CWE-304 Missing Critical Step in Authentication

18. CWE-305 Authentication Bypass by Primary Weakness

19. CWE-306 Missing Authentication for Critical Function

20. CWE-307 Improper Restriction of Excessive Authentication Attempts

21. CWE-308 Use of Single-factor Authentication

22. CWE-309 Use of Password System for Primary Authentication

23. CWE-346 Origin Validation Error

24. CWE-350 Reliance on Reverse DNS Resolution for a Security-Critical Action

25. CWE-384 Session Fixation

26. CWE-521 Weak Password Requirements

27. CWE-613 Insufficient Session Expiration

28. CWE-620 Unverified Password Change

29. CWE-640 Weak Password Recovery Mechanism for Forgotten Password

30. CWE-798 Use of Hard-coded Credentials

31. CWE-940 Improper Verification of Source of a Communication Channel

32. CWE-941 Incorrectly Specified Destination in a Communication Channel

33. CWE-1390 Weak Authentication

34. CWE-1391 Use of Weak Credentials

35. CWE-1392 Use of Default Credentials

36. CWE-1393 Use of Default Password

  

# A08:2025 - Software or Data Integrity Failures

1. CWE-345 Insufficient Verification of Data Authenticity

2. CWE-353 Missing Support for Integrity Check

3. CWE-426 Untrusted Search Path

4. CWE-427 Uncontrolled Search Path Element

5. CWE-494 Download of Code Without Integrity Check

6. CWE-502 Deserialization of Untrusted Data

7. CWE-506 Embedded Malicious Code

8. CWE-509 Replicating Malicious Code (Virus or Worm)

9. CWE-565 Reliance on Cookies without Validation and Integrity Checking

10. CWE-784 Reliance on Cookies without Validation and Integrity Checking in a Security Decision

11. CWE-829 Inclusion of Functionality from Untrusted Control Sphere

12. CWE-830 Inclusion of Web Functionality from an Untrusted Source

13. CWE-915 Improperly Controlled Modification of Dynamically-Determined Object Attributes

14. CWE-926 Improper Export of Android Application Components

  

# A09:2025 - Security Logging and Alerting Failures

1. CWE-117 Improper Output Neutralization for Logs

2. CWE-221 Information Loss of Omission

3. CWE-223 Omission of Security-relevant Information

4. CWE-532 Insertion of Sensitive Information into Log File

5. CWE-778 Insufficient Logging

  

# A10:2025 - Mishandling of Exceptional Conditions

1. CWE-209 Generation of Error Message Containing Sensitive Information

2. CWE-215 Insertion of Sensitive Information Into Debugging Code

3. CWE-234 Failure to Handle Missing Parameter

4. CWE-235 Improper Handling of Extra Parameters

5. CWE-248 Uncaught Exception

6. CWE-252 Unchecked Return Value

7. CWE-274 Improper Handling of Insufficient Privileges

8. CWE-280 Improper Handling of Insufficient Permissions or Privileges

9. CWE-369 Divide By Zero

10. CWE-390 Detection of Error Condition Without Action

11. CWE-391 Unchecked Error Condition

12. CWE-394 Unexpected Status Code or Return Value

13. CWE-396 Declaration of Catch for Generic Exception

14. CWE-397 Declaration of Throws for Generic Exception

15. CWE-460 Improper Cleanup on Thrown Exception

16. CWE-476 NULL Pointer Dereference

17. CWE-478 Missing Default Case in Multiple Condition Expression

18. CWE-484 Omitted Break Statement in Switch

19. CWE-550 Server-generated Error Message Containing Sensitive Information

20. CWE-636 Not Failing Securely ('Failing Open')

21. CWE-703 Improper Check or Handling of Exceptional Conditions

22. CWE-754 Improper Check for Unusual or Exceptional Conditions

23. CWE-755 Improper Handling of Exceptional Conditions

24. CWE-756 Missing Custom Error Page