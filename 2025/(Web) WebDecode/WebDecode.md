# <u>WebDecode</u>
> *Do you know how to use the web inspector?
Start searching here to find the flag*

![CTF Details](/2025/(Web)%20WebDecode/screenshots/details.png)

## About the Challenge
This is a web exploitation CTF found at `https://play.picoctf.org/practice/challenge/427`. After running the instance, we were allowed to access a webpage at `http://titan.picoctf.net:63032/`.

Upon navigating to the website, we are greeted with this page.
![Web Server Landing Page](/2025/(Web)%20WebDecode/screenshots/homepage.png)

## How to Solve?
Time to test this website out!

Nothing on the `index.html` endpoint, so lets naviagate to the About tab on the header.
![About Page](/2025/(Web)%20WebDecode/screenshots/about.png)
Looks like we are given a small hint, telling us to inspect the page.

Lets open up developer tools and start some inspecting.

After inspecting some of the source code of the `about.html` endpoint, we find what looks like a Base64 encoded string in the attributes of one of the sections.
![About Page Source Code](/2025/(Web)%20WebDecode/screenshots/sourcecode.png)

The encoded string we found is `cGljb0NURnt3ZWJfc3VjYzNzc2Z1bGx5X2QzYzBkZWRfMDdiOTFjNzl9`.

### Decrypting the encoded Base64 string
Lets use CyberChef to decode the encoded string we found.

Using the `Magic` function makes this process much easier as it does the hashing algorithm detection and decryption all at once.
![CyberChef Decryption](/2025/(Web)%20WebDecode/screenshots/cyberchef.png)

As we can see, we were correct about the Base64 encrpytion, and decrypting it has provided us the flag for this challenge!

### Flag Found!
```
picoCTF{web_succ3ssfully_d3c0ded_07b91c79}
```