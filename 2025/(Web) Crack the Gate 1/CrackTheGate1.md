# <u>Crack the Gate 1</u>
> *We’re in the middle of an investigation. One of our persons of interest, ctf player, is believed to be hiding sensitive data inside a restricted web portal. We’ve uncovered the email address he uses to log in: `ctf-player@picoctf.org`. Unfortunately, we don’t know the password, and the usual guessing techniques haven’t worked. But something feels off... it’s almost like the developer left a secret way in. Can you figure it out?
Additional details will be available after launching your challenge instance.*


## About the Challenge
This is a web exploitation CTF found at `https://play.picoctf.org/practice/challenge/520`. After running the instance, we were allowed to access a webpage at `http://amiable-citadel.picoctf.net:62027/`.

Here is what it looks like...
![Initial Webpage](/2025/(Web)%20Crack%20the%20Gate%201/screenshots/initial_webpage.png)

## How to Solve?
This is my ***first ever CTF***, but I do know some basic web exploitation techniques.

The hint provided in the challenge description, "...it’s almost like the developer left a secret way in", caught my attention and led me to inspect the page's source code.

After quick inspection, I found a commented line that was left behind by the developer.
![Webpage Source Code](/2025/(Web)%20Crack%20the%20Gate%201/screenshots/source_code.png)

The line "***ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf"***" seems to be of importance, but of course it is encoded.

The format doesn't seem like any complex hashing technique or algorithm, so lets go to CyberChef and try to ***brute force a Caesar Cypher***. I use the brute force option so that I can see all possible shifts at once.
![CyberChef Caesar Cypher](/2025/(Web)%20Crack%20the%20Gate%201/screenshots/cyberchef.png)

Here we can see we were right about the encoding algorithm used!

A shift of 13 results in ***Amount = 13: NOTE: Jack - temporary bypass: use header "X-Dev-Access: yes"***.

To be able to intercept network traffic and use the header we found, we are going to use **Burp Suite**. 

## Using Burp Suite to Intercept and Modify HTTP Traffic

*Burp Suite's intercept feature allows us to capture, view, and modify HTTP requests and responses between a web browser and a web server, acting as a proxy.*

Going into Burp Suite, we are going to first go to the Proxy tab and open a Burp Browser.

Following this, we will navigate to the webpage we are trying to break into.

Using the provided email (`ctf-player@picoctf.org`) and a random password (`test`), we will first turn on intercept mode on Burp Suite, and then send the form.

You will see that the webpage continues to refresh, but the "Request" field in Burp Suite gets populated. This is where we will add our temporary bypass of ***X-Dev-Access: yes***.
![Burp Suite Header Bypass](/2025/(Web)%20Crack%20the%20Gate%201/screenshots/burp_request.png)

Now, forward this header to the web server by clicking the orange "Forward" button.

The request goes through with the intercepted/updated header, and returns us the flag through an alert.
![Flag Alert](/2025/(Web)%20Crack%20the%20Gate%201/screenshots/flag.png)

***First CTF completed!***

### Flag Found!
```
picoCTF{brut4_f0rc4_83812a02}
```