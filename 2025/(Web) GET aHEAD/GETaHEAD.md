# <u>GET aHEAD</u>
> *Find the flag being held on this server to get ahead of the competition http://mercury.picoctf.net:53554/*

![CTF Details](/2025/(Web)%20GET%20aHEAD/screenshots/details.png)

## About the Challenge
This is a web exploitation CTF found at `https://play.picoctf.org/practice/challenge/132`. We are also given a webpage to access at `http://mercury.picoctf.net:53554/`.

Upon navigating to the website, we are greeted with this page.
![Web Server Landing Page](/2025/(Web)%20GET%20aHEAD/screenshots/start.png)

## How to Solve?
Time to test this website out!

Testing some functionality of the webpage, clicking the buttons simply changes the background color of the webpage from red to blue, no URL changes or anything.

Lets dive a little deeper and use developer tools to inspect the source code.

Some inspection of the source code reveals that the webpage sends a `GET` request to web server if the `Choose Red` button is clicked.

In contrast, the `Choose Blue` button results in a `POST` request to the web server to update the background from red to blue.

### Using Burp Suite to Intercept HTTP Requests
Lets use Burp Suite to analyze requests.

We find that the `GET` and `POST` requests do not contain any valuable information.

However, thinking about the title of the challenge, `GET aHEAD`, we can focus our attention on another HTTP method to help us out, the `HEAD` method.

The HTTP `HEAD` method is similar to the `GET` method, however the response is simply just HTTP headers and resource metadata. 

Using Burp Suite to intercept a HTTP request and changing the request to be a `HEAD` HTTP request and then analyzing the response gets us our flag!
![Flag Found](/2025/(Web)%20GET%20aHEAD/screenshots/head_request.png)

### Flag Found!
```
picoCTF{r3j3ct_th3_du4l1ty_2e5ba39f}
```