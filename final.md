
## DEFENSE AGAINST THE DARK ARTS
### CS373 - SUMMER 2019
<br>
[Week 2](index.md)  [Week 3](week3.md)  [Week 4](week4.md)  [Week 5](week5.md)  [Week 6](week6.md)  [Homework 3](homework3.md)
[Week 7](week7.md)  [Week 8](week8.md)

<br><br>
## Final: Hack The Box

### Obtain HTB Account

To join HTB go here:  https://www.hackthebox.eu/invite

To get an account with HTB takes more work than simplly entering an email and password. This site is for practicing penetration skills so it's fitting that you need to hack your own way in. More specifically, you have to generate an invitation code.

For my first attempt to create my invite code, I wanted to do something silly and see what happens. My inspiration was from the Little Bobby Tables comic on SQL injection and a character from Stranger Things. “Barb’); DROP TABLE USERS” as I expected, didn’t do anything but return an invalid invite code message.

![littleBobby](littleBobby.JPG) ![InviteCode1](InviteCode1.JPG)
<br>


My next attempt used some SQL injection that would hopefully evaluate to true and get me authenticated. Unfortunately, this returned some unwelcomed results. I was temporarily blocked by HTB.

![invite_attempt2](invite_attempt2.JPG)
<br>

![beenBlocked](beenBlocked.JPG)
<br>


Once, I was unblocked I inspected the Sign-Up page and noticed a source script “/js/inviteapi.min.js” that looked promising. 

![InviteCodeInspect](InviteCodeInspect.JPG)
<br>


I entered the path and found the source code and saw a function called “makeInviteCode”. That's exactly what I wanted to do.

![inviteapi](inviteapi.JPG)
<br>

Back on the original sign-up page in the console, I entered “makeInviteCode()”. The response included a string in the data entity. 

![makeInviteCode](makeInviteCode.JPG)
<br>


I attempted to use the string as the invite code but that failed. The encrypt type of the string is Base64, so I went to a site to https://www.base64decode.org/ to decrypt, and the following instructions were decoded: “In order to generate the invite code, make a POST request to /api/invite/generate.

![decodebase64](decodebase64.JPG)
<br>


Using Postman I made the POST request, which returned a code. 

![Inkedpostman](Inkedpostman.jpg)
<br>


This code did not work on the sign-up page, so I went back to the decode Base64 page. Once I decoded the code, I went back to the sign-up page and successfully signed up to HTB!


![loginCongrats](loginCongrats.JPG)
<br><br>


### References



