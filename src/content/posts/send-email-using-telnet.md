---
title: "Send Email Using Telnet"
date: 2018-05-17T10:47:34+02:00
draft: true
---

Sometimes you need to check if a SMTP server is functioning correctly.
This can be easily archived using telnet:

```
telnet <SMTP_SERVER> 25

EHLO <SMTP_SERVER>
MAIL FROM: <FROM_EMAIL_ADDRESS>
RCPT TO: <TO_EMAIL_ADDRESS>
DATA
Subject: Test
<ENTER>
<ENTER>
This is a test email.
<ENTER>
<ENTER>
.
QUIT
```