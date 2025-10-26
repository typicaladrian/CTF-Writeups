# <u>Bookmarklet</u>
> *Why search for the flag when I can make a bookmarklet to print it for me?
Browse here, and find the flag!*

![CTF Details](/2025/(Web)%20Bookmarklet/screenshots/details.png)

## About the Challenge
This is a web exploitation CTF found at `https://play.picoctf.org/practice/challenge/406`. After running the instance, we were allowed to access a webpage at `http://titan.picoctf.net:55112/`.

Upon navigating to the website, we are greeted with this page.
![Web Server Landing Page](/2025/(Web)%20Bookmarklet/screenshots/start.png)

## How to Solve?
First, due to the title and initial starting page, we need to understand what a **bookmarklet** is.

A **bookmarklet** is a browser bookmark that executes JavaScript instead of opening a webpage. These bookmarklets can also be known as *bookmark applets, favlets, or JavaScript bookmarks*.

Using this knowledge, lets create a bookmarklet using the code provided in the starting page.
![Creation of booklet](/2025/(Web)%20Bookmarklet/screenshots/create_booklet.png)

After creating the booklet and executing it, we are provided with the flag!
![Executing booklet to obtain flag](/2025/(Web)%20Bookmarklet/screenshots/flag.png)

### Flag Found!
```
picoCTF{p@g3_turn3r_0148cb05}
```