# Session
Related: [cookies](../../C/cookies)

## How a session works
1. a user accesses the web server using a web browser.
2. The web server side issues a session ID and associates it with the accessing user.
3. The Web server issues a session ID and associates it with the user.
4. When the user accesses the same web server again, the saved cookie is sent.
5. The web server side receives the cookie, examines the session ID, and retrieves the associated user data. 

### Flow to login
1. ask the user to log in with ID and password. (A user who has not logged in does not have a session ID.)
2. If the authentication is successful, the server creates a session ID. After successful authentication, the server creates a session ID, which is a long random number that is difficult to guess.
3. In order to link the session ID and user information, the server stores the generated session ID and user ID as a pair in a database such as Redis.
4. save the generated session ID in a cookie.

### Points
- By storing only the session ID and not the information in the cookie, there will be no problem even if it is stolen.
- The memory to restore the state based on the session ID is on the web server, so it is highly secure.
- You don't have to worry about the limitation of the amount of information that can be stored in a cookie.

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