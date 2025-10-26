# <u>Unminify</u>
> *I don't like scrolling down to read the code of my website, so I've squished it. As a bonus, my pages load faster!
Browse here, and find the flag!*

![CTF Details](/2025/(Web)%20Unminify/screenshots/description.png)

## About the Challenge
This is a web exploitation CTF found at `https://play.picoctf.org/practice/challenge/426`. After running the instance, we were allowed to access a webpage at `http://titan.picoctf.net:49262/`.

Upon navigating to the website, we are greeted with this page.
![Web Server Landing Page](/2025/(Web)%20Unminify/screenshots/landing_page.png)

## How to Solve?
Time to test this website out!

First, lets just investigate the source code and HTML using basic dev tools.

We find that this challenge turns out to be fairly simple, with the flag being hidden as a class attribute in a random HTML `<p>` tag.
![Flag Found in HTML](/2025/(Web)%20Unminify/screenshots/flag.png)

### Flag Found!
```
picoCTF{pr3tty_c0d3_d9c45a0b}
```