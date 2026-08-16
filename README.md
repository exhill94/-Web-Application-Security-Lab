# Web Application Security Lab

## Objective
Practice identifying and validating common web application vulnerabilities.

## Tools
- Burp Suite Community Edition
- DVWA
- Kali Linux

## Testing Performed
- Intercepted HTTP requests with Burp Proxy
- Modified requests with Repeater
- Tested for SQL injection
- Tested broken access control / IDOR
- Reviewed authentication and input handling

## Example Finding
A user-controlled identifier could be modified to retrieve data belonging to another user, demonstrating broken access control.

## Remediation
Enforce server-side authorization checks for every requested resource.

## What I Learned
- Authentication and authorization are different
- Client-side controls should not be trusted
- Vulnerabilities should be manually reproduced before being reported
