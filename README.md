# SQL Injection Analysis – DVWA (Medium Security)

## Overview
This project documents a security analysis of the SQL Injection module in DVWA (Damn Vulnerable Web Application) at Medium security level.

---

## Application Architecture

`User Input → Application Server → SQL Query → Database`

The vulnerability existed in how user input was concatenated into SQL statements.

---

## Defense Observed

Medium level implemented:
`mysqli_real_escape_string()`

However, this only escapes quotes.

---

## Exploitation Steps

1. Intercepted POST request via Burp Suite
2. Modified numeric parameter
3. Injected logical payload: `1 OR 1=1`
4. Extracted entire user table
5. Retrieved database metadata

---

## Root Cause

User input concatenated directly into SQL query without parameterization.

---

## Impact

- Data exfiltration
- Credential hash exposure
- Database fingerprinting

---

## Proper Fix

- Use Prepared Statements
- Parameterized Queries
- Strict input typing
- Least privilege database accounts

---

## Key Takeaway

Blacklisting characters is not security.  
Query parameterization is mandatory.
