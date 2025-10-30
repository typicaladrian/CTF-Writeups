# <u>Local Authority</u>
> *Can you get the flag?
Go to this website and see what you can discover.*

![CTF Details](/2025/(Web)%20Local%20Authority/screenshots/details.png)

## About the Challenge
This is a web exploitation CTF found at `https://play.picoctf.org/practice/challenge/278`. After running the instance, we were allowed to access a webpage at `http://saturn.picoctf.net:56566/`.

Upon navigating to the website, we are greeted with this page.
![Web Server Landing Page](/2025/(Web)%20Local%20Authority/screenshots/start.png)

## How to Solve?
Time to test this website out!

First, lets just investigate the source code and HTML using basic dev tools.

Inspecting the login page source code doesn't reveal much if anything.

Lets try to log in. I tested the username `admin` and the password `password`.
Unfortunately, but as expected, it looks like we entered in an incorrect password.
![Failed Log In Page](/2025/(Web)%20Local%20Authority/screenshots/failed_login.png)

Lets inspect the source code of this page.

Towards the top of the source code, we can see that there is actually a hidden form that routes to `admin.php`.
![Hidden Form Source Code](/2025/(Web)%20Local%20Authority/screenshots/admin_endpoint.png).
The main thing to note is that it appears that we can only access this endpoint if we match the required id, which is `hash` being the `adminFormHash` value. We just need to figure out what value we need.

### Locally Stored Hash Value

Continuing our investigation of the failed login page gives us exactly what we need.
![Exposed Hash In Source Code](/2025/(Web)%20Local%20Authority/screenshots/exposed_hash.png)
Looks like if the user inputs the correct username and password, log in is successful and the `adminFormHash` value is used to grant access to the `admin.php` page.

In this scenario, the developers should NOT have stored this hash value locally in the public source code.

After some testing however, it seems like the `admin.php` endpoint does not accept `GET` requests, meaning we cannot simply pass the hash through URL attributes to access the authorized endpoint.

Red herring?

### Moving onto Burp Suite
Lets open up Burp Suite and use it to try and find out more information about this web server.

Navigating to the webpage and trying to login builds some of our site map through Burp, which ends up revealing a new URL that we were not aware of before `secure.js`.
![Secure.js Revealed Through Burp Site Map](/2025/(Web)%20Local%20Authority/screenshots/burp.png)

Looks like the admin password was hardcoded into this page, which we can now use to access the authorized webpage.
![Flag Found](/2025/(Web)%20Local%20Authority/screenshots/flag.png)

### Flag Found!
```
picoCTF{j5_15_7r4n5p4r3n7_b0c2c9cb}
```