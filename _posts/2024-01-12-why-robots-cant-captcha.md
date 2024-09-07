---
layout: article
title: "Why AIs can't reCAPTCHA?"
excerpt: "Robots a.k.a AIs can do a lot of things, but why not pass the captcha box test...."
date: 2023-05-02
tags:  [AI, Cybersecurity]
mathjax: false
mathjax_autoNumber: false
key: why-ai-cant-recaptcha
---

<div align="center">
  <img src="https://raw.githubusercontent.com/is-this-echo/blog-img-hosting/main/images/recaptcha-robot.png" alt="reCaptcha logo" width="30%">
</div>


> #### CAPTCHA : Completely Automated Public Turing test to tell Computer and Humans Apart


Background
---
 In the initial days, CAPTCHAs used to look like this :
 <div align="center">
  <img src="https://raw.githubusercontent.com/is-this-echo/blog-img-hosting/main/images/captcha-2.jpg" alt="Ancient CAPTCHA" width="40%">
</div>


As AIs became smarter, the difficultly levels of the CAPTCHA increased to the point
where humans were not able to solve them anymore 😭.

<div align="center">
  <img src="https://raw.githubusercontent.com/is-this-echo/blog-img-hosting/main/images/captcha-promax.jpg" alt="Unreadable CAPTCHA" width="40%">
</div>

*Advanced OCRs, image/object detection* algorithms made it easy for AI bots to pass the test
leading to more spam, data scraping and brute force password cracking on websites.
Spammers have even resorted to outsourcing CAPTCHA solving to groups of low-wage "human" workers
in Russia and Southeast Asia (with rates as low as 0.30 USD per 1k traditional CAPTCHAs).


So what's up with the new reCAPTCHA box test developed by Google?
---

We just need to click the box to pass the test, looks very simple, isn't it...
AIs can easily do that.
Well the real test is not the click but what you do before the click- **how the mouse cursor 
moves towards the box**. This behaviour is tracked by Google using javascript.
A bot or AI usually reaches the destination in ***straight path(s)*** (horizontal or vertical)
whereas for us it's not so straight, you know what I mean 😁.
Also, conventional bots are more likely to click on the **centre pixel** inside the box but not us.

<div align="center">
  <img src="https://raw.githubusercontent.com/is-this-echo/blog-img-hosting/main/images/captcha-human-bot.png" alt="Cursor tracking comparison" width="100%">
</div>

This cursor tracking algo is also used in **image-based reCAPTCHAs** where you pass the test even if you didn't correctly label all instances of the requested object.
(Btw, rates for solving these for human workers are 1.05 USD per 1k reCAPTCHAs).

But, this doesn't stop here, I bet the next piece of info I am gonna provide will surprise you.
Google also uses your **search history** to find out if you are indeed not a robot.
(Check out Google's privacy policy if you are curious!)

<div align="center">
  <img src="https://raw.githubusercontent.com/is-this-echo/blog-img-hosting/main/images/evolution-of-captcha.png" alt="Evolution of CAPTCHA" width="100%">
</div>

Now that you know about working of reCAPTCHAs, hope it will protect
our websites for the time being until AGI takes over in the future, which could lead to 
the possibility of having to use biometric or face unlock :(

---
If you like TeXt, don't forget to give me a star. :star2:

[![Star This Project](https://img.shields.io/github/stars/is-this-echo/is-this-echo.github.io.svg?label=Stars&style=social)](https://github.com/is-this-echo/is-this-echo.github.io)
