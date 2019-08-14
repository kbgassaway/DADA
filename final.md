
## DEFENSE AGAINST THE DARK ARTS
### CS373 - SUMMER 2019
<br>
[Week 2](index.md)  [Week 3](week3.md)  [Week 4](week4.md)  [Week 5](week5.md)  [Week 6](week6.md)  [Homework 3](homework3.md)
[Week 7](week7.md)  [Week 8](week8.md)

<br><br>
## Final: Hack The Box

Hack The Box (HTB) is an online platform for testing and advancing your penetration skills. Challenges range in difficulty so hackers of all skill levels are welcome. HTB has their own private messaging system and forums so that you can get hints and encouragement along the way. I'll cover obtaining an HTB account and three challenges.
<br>

### Obtain HTB Account

To join HTB go here:  https://www.hackthebox.eu/invite

To get an account with HTB takes more work than simplly entering an email and password. This site is for practicing penetration skills so it's fitting that you need to hack your own way in. More specifically, you have to generate an invitation code.

For my first attempt to create my invite code, I wanted to do something silly and see what happens. My inspiration was from the Little Bobby Tables comic on SQL injection and a character from Stranger Things. “Barb’); DROP TABLE USERS” as I expected, didn’t do anything but return an invalid invite code message.

![littleBobby](littleBobby.JPG)![InviteCode1](InviteCode1.JPG)
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


This code did not work on the sign-up page, so I went back to the decode Base64 page. Once I decoded the code, I went back to the sign-up page and successfully signed up to HTB! Once you have successfully created your invite code, you may create a user account. Don't worry, you won't have to create your own invite code each time you want to login.

![loginCongrats](loginCongrats.JPG)
<br>


Before you get started, it's important that you read the rules so that you don't get into any legal trouble. It's also highly recommended that you use a virtual machine and vpn using the provided connection pack as HTB cannot gaurentee that the site or the files contain no malicious content. The vm I built runs Ubuntu using VirtualBox.
<br><br>

### MarketDump      by butrintkomoni    \[30 Points]

"We have got informed that a hacker managed to get into our internal network after pivoiting through the web platform that runs in public internet. He managed to bypass our small product stocks logging platform and then he got our costumer database file. We believe that only one of our costumers was targeted. Can you find out who the customer was?"

MarketDump is a Forensics challenge. The zip file contains a pcapng file, a network traffic dump file. If you open in a text editor or cat out in your terminal, you will see thousands of American Express card numbers listed. While scrolling through the card list I found one credit card number that stood out - it was alphanumeric and over twice the length of the other card numbers. This must be the customer who was targeted so I copied the string to a text file.

![mD2](mD2.JPG)
<br>

Easy 30 points, I thought, just decode the string using Base64 and get the flag to submit. Wrong. Decoding using Base64 returns invalid input.

![mD3](mD3.JPG)
<br>

I heard about the toolkit website for decryption, (dcode.fr)[https://www.dcode.fr/about], from a classmate, and attempted to decode the string using Base26 and Base36. Unforetunately, both of these resulted in garbage. The flag to submit needs to be in the format of HTB{...}.

![mD4](mD4.JPG)
<br>

I searched for other decoding tools online and found (CyberChef)[https://gchq.github.io/CyberChef/], an open source web tool designed for decoding data. This tool can automatically determine which what method to use to decode your input, perhaps based on the combination of the input itself and the output after decoding. I placed the string in the input, keep Auto Bank checked, hit bake, and the decoded flag appears! 

![mD5](mD5.JPG)
<br>

CyberChef lets you know what method they used to decode the text. In this case it was Base58, which I was not familiar with. Base58 is an alphanumeric set of characters that leaves out letters and numbers that are more difficult to transcribe, such as 0, O, I, l. Base58 is used in bitcoin transactions (https://learnmeabitcoin.com/glossary/base58).

Input the flag in the MarketDump challenge and submit.

![mD6](mD6.JPG)
<br>

### References



