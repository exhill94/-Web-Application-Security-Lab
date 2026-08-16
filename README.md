# Web Application Security Lab

## Overview

This home lab documents hands-on web application security testing using
Burp Suite Community Edition and intentionally vulnerable web applications.

The goal of the lab was to better understand how web vulnerabilities work,
how HTTP requests can be manipulated, and how potential vulnerabilities can
be manually validated rather than relying only on automated tools.

## Lab Environment

- Kali Linux
- Burp Suite Community Edition
- DVWA (Damn Vulnerable Web Application)
- Isolated virtual lab network
- Web browser configured to proxy traffic through Burp Suite

## Objectives

- Understand HTTP requests and responses
- Intercept application traffic using Burp Proxy
- Modify and resend requests using Burp Repeater
- Test application inputs for common web vulnerabilities
- Validate whether suspicious behavior represents a real vulnerability
- Understand the potential impact of identified vulnerabilities

## Burp Suite Workflow

I configured my browser to send web traffic through Burp Suite.

Using **Proxy**, I was able to intercept requests between the browser and
the web application and inspect parameters, headers, cookies, and other
request data.

Interesting requests were then sent to **Repeater**, where I could modify
individual values and resend the request while comparing the application's
responses.

This allowed me to manually test how the server handled unexpected or
manipulated input.

## SQL Injection Testing

One exercise involved a user lookup function that accepted a user-controlled
ID value.

I intercepted the request and modified the input to determine whether
user-controlled data could influence the underlying database query.

The application's response changed in a way that demonstrated the input was
being interpreted as part of the SQL query rather than being safely handled
as data.

### Potential Impact

SQL injection can potentially allow an attacker to:

- Access data they are not authorized to view
- Enumerate database information
- Modify or delete data depending on database permissions
- Compromise application confidentiality and integrity

### Remediation

Applications should use parameterized queries / prepared statements rather
than constructing SQL queries directly from user-controlled input.

Input validation should also be implemented as an additional defensive
control.

## Broken Access Control Testing

I also practiced testing authorization controls by manipulating object
identifiers contained within application requests.

For example, if an authenticated user requests a resource using an identifier,
the server should verify that the authenticated user is actually authorized
to access that specific resource.

Changing an identifier and receiving another user's protected resource would
indicate a potential broken access control / IDOR vulnerability.

### Key Lesson

Authentication and authorization are separate security controls.

**Authentication:** Who is the user?

**Authorization:** What is that user allowed to access or perform?

Authorization decisions should always be enforced server-side rather than
trusting values supplied by the client.

## Key Takeaways

- Burp Proxy provides visibility into communication between a browser and
  web application.
- Burp Repeater makes it possible to manually manipulate and repeatedly test
  individual requests.
- Automated findings and suspicious behavior should be manually investigated
  when appropriate.
- User-controlled input should never automatically be trusted.
- Authentication does not guarantee proper authorization.
- Understanding the application's normal behavior makes abnormal behavior
  easier to identify.
- Demonstrating actual impact provides more useful information than simply
  identifying a vulnerability category.

## Disclaimer

All security testing documented in this repository was performed in an
isolated home lab against intentionally vulnerable applications for
educational purposes.
