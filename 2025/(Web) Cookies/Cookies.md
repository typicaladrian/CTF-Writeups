# <u>Cookies</u>
> *Who doesn't love cookies? Try to figure out the best one. http://mercury.picoctf.net:6418/*

![CTF Details](/2025/(Web)%20Cookies/screenshots/details.png)

## About the Challenge
This is a web exploitation CTF found at `https://play.picoctf.org/practice/challenge/173`. After running the instance, we were allowed to access a webpage at `http://mercury.picoctf.net:6418/`.

Upon navigating to the website, we are greeted with this page.
![Web Server Landing Page](/2025/(Web)%20Cookies/screenshots/start.png)

## How to Solve?
Time to test this website out!

Inputting `snickerdoodle` and hitting search leads us to a `/check` endpoint that looks like this.
![Test input](/2025/(Web)%20Cookies/screenshots/testing.png)

Seems pretty basic, except we have now found a new endpoint that can be of use to us.

It is also important to note that inputting something that is not a valid cookie, like the word `test`, gives us an error message.
![Failure input](/2025/(Web)%20Cookies/screenshots/invalid.png)

Hint, hint! This may be important to us later since it shows that some type of search is being made to ensure that the cookie is valid, maybe a cookie database is stored in the backend? ***If we are able to traverse through the cookie database, we may be able to find our flag!*** 

First, lets just investigate the source code and HTML using basic dev tools.

Looks like there's nothing hidden in the source code, so now lets move into Burp Suite to inspect HTTP requests.

### Using Burp Suite to Investigate HTTP Requests
Using the Burp Suite browser, lets navigate to the Cookies webpage and build a site map and HTTP history using an input of `snickerdoodle`.

We see from the history that after clicking the "Search" button with a valid input, a `POST` request is made to the `/search` endpoint with a body of `name=snickerdoodle`.
![POST search request](/2025/(Web)%20Cookies/screenshots/search.png)

Analyzing the response also shines light on the fact that this endpoint simply redirects to the target to `/check` after verification that the user input can be associated with a cookie stored in the server.

Analyzing the following `GET` request to the `/check` endpoint tells the full story.
![Check Endpoint Data](/2025/(Web)%20Cookies/screenshots/check.png)

The `Cookie: name=0` request header caught my attention, so I decided to play around with it.

We know that `name=0` is the index for the snickerdoodle cookie, so what if we set `name=1`?

Using the Burp Suite repeater, we can resend this `GET` request to `/check` with an updated `Cookie` value.
![Cookie value manipulation](/2025/(Web)%20Cookies/screenshots/name_manip.png)
As we hypothesized, changing the `Cookie` value manually and resending the `GET` request allows us to iterate through valid cookie values *without actually knowing what cookies are valid cookie values!*

So exciting! Now, all we should have to do is iterate through all the cookie indicies until we find the flag.

And just as we expected, at `Cookie: name=18` we obtained a flag!
![Flag found](/2025/(Web)%20Cookies/screenshots/flag.png)

*Note: I learned after reading a writeup for this challenge that Burp Intruder could have been used to automate the process of testing all `Cookie` values using simple Python scripts. The more you know! Can't wait to use this feature in the future!*


### Flag Found!
```
picoCTF{3v3ry1_l0v3s_c00k135_88acab36}
```