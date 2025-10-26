# <u>Cookie Monster Secret Recipe</u>
> *Cookie Monster has hidden his top-secret cookie recipe somewhere on his website. As an aspiring cookie detective, your mission is to uncover this delectable secret. Can you outsmart Cookie Monster and find the hidden recipe?
You can access the Cookie Monster here and good luck*

![CTF Details](/2025/(Web)%20Cookie%20Monster%20Secret%20Recipe/screenshots/details.png)

## About the Challenge
This is a web exploitation CTF found at `https://play.picoctf.org/practice/challenge/469`. After running the instance, we were allowed to access a webpage at `http://verbal-sleep.picoctf.net:61595/`.

Upon navigating to the website, we are greeted with this page.
![Web Server Landing Page](/2025/(Web)%20Cookie%20Monster%20Secret%20Recipe/screenshots/landing_page.png)

## How to Solve?
Time to test this website out!

Just putting in some basic information and sending the request to the web server redirects us to the following page...
![Testing Website](/2025/(Web)%20Cookie%20Monster%20Secret%20Recipe/screenshots/testing_site.png)

Nothing special here, except for the hint: `Hint: Have you checked your cookies lately?`

Honestly, we could've guessed from the title of the challenge that we were going to have to do some cookie inspection.

Lets open up the browser dev tools, in this case Microsoft Edge's Developer Tools, head over to the Application tab, and view cookie data.
![Cookie Data](/2025/(Web)%20Cookie%20Monster%20Secret%20Recipe/screenshots/cookie.png)

As we can see, a secret cookie was stored!

The value of `cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlc19jMDBraWVzX0E2RkEwN0Q4fQ==` for the secret cookie looks like a Base64 encoded string.

### Decrypting
From this stage, we can go to a website to first identify the hash, but CyberChef has a nifty tool that automatically detects properties of given inputs and suggests which operations would be most beneficial to perform. This operation is called `Magic`.

Lets test it on this string!
![CyberChef Decrypting](/2025/(Web)%20Cookie%20Monster%20Secret%20Recipe/screenshots/cyberchef.png)

As we can see, the `Magic` operation detected the input as a Base64 encoded string and automatically decrypted it for us, giving us our flag for the challenge.

### Flag Found!
```
picoCTF{c00k1e_m0nster_l0ves_c00kies_A6FA07D8}
```