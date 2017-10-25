---
layout:     post
title:      "Prevent Pwned Passwords"
subtitle:   "The easy way to avoid bad passwords"
date:       2017-10-24 12:00:00
author:     "Chris"
header-img: "img/home-bg.jpg"
---

As more and more data breaches occur, it becomes more and more difficult to keep passwords secure. One of the [emerging recommendations
among experts](https://www.troyhunt.com/passwords-evolved-authentication-guidance-for-the-modern-era/) is to use passwords that have never been involved in any breach. This can be a bit overwhelming -- it means that you should
never use a password that anyone (not just yourself) has ever used that's been hacked. There are hundreds of millions (if not more)
passwords that have been leaked over time -- that's a lot of passwords you need to make sure you don't use.

Why do you want to avoid any password that's ever been in a breach, even if it was with someone else's account? If amalicious hacker wants
to try to find some credentials to use somewhere, they may try a brute force attack. That is, they have an automated process that tries
as many passwords as possible. So they might start with "aaaaaaaa", then "aaaaaaab", then "aaaaaaac", and so on. With that approach, it
takes a lot of tries to stumble onto a successful password for an account. But they could build a dictionary of all the passwords that
have been used in breaches and start by trying those passwords first -- this approach is far more likely to generate working credentials
far more quickly.

To help you avoid using breached passwords, I've created a Chrome extension. Anytime you enter a password -- whether logging in to a site,
creating an account, or changing your password -- it'll check your password against a [known list of breached passwords](https://haveibeenpwned.com/Passwords) and display a notification if that password has been used in a previous breach. If it gives you an
alert, you should change that password ASAP.
