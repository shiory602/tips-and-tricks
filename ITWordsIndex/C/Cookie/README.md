# Cookies
Related: [Session](../../S/Session), [HTTP](../../../front-end-tips/1.internet/WhatisHTTP)

### My understanding.
> A memory function on the web browser side that remembers what you've done when you access the web server.

## What are cookies?
Cookies are an extension of the HTTP specification that allows information to be exchanged between web applications and web browsers**.
A cookie is a piece of information made up of a combination of "name = value" that is sent from a web server to a web browser using the header of an HTTP response.
> A cookie is a piece of information stored in a web browser (client).
When a web browser receives a cookie from a web server, it sends the received cookie as is in the HTTP request header the next time it accesses the same web server.
> The state of the client side (Wev browser) is maintained based on the cookie information.
## Problems with cookies
Cookies are not secure because they can be easily looked into by using certain tools!
Therefore, a way to keep more information more securely was devised: "[Session](../../S/Session)" mechanism.

## Difference between Cookie and Session
| Features | Session | Cookie |
| --- | --- | --- |
| Where data is stored | In the server | In the user's PC (per web browser) |
| Storage capacity of data | Almost unlimited (maximum is up to disk space) | Limited (1 application: 4096Byte*20)
| Data storage format | Program data format | Character string (text file) |
| Expiration date | Fixed (until the web browser closes or the time in the configuration file | Set arbitrarily) |
| Security aspects | Less dangerous than cookies | More dangerous |
| Use of data | Can be used immediately after storing it | Can be used after re-requesting it |

***

Reference: [Umaro's Game Blog](https://umaroidblog.com/webtechnology1),
[Let's use cookies and sessions](https://kanda-it-school-kensyu.com/php-basic-contents/pb_ch11/pb_1103/),
[How sessions work on ordinary web sites](https://blog.kozakana.net/2017/08/about_web_session/)