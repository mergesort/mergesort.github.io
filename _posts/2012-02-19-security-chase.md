---
layout: post
title: Security Chase
tags: [industry, programming]
---

Go to your Chase account and enter your password. Now log out, and enter your password with a different pattern of capitalization. So if your password was `Password`, now try `pASSWORD`. I bet you it worked and Chase still let you into your account. 

>I’ll preface the coming diatribe with a statement about my expertise. I am not a security researcher and would never call myself an expert in the field of cryptography. I’m just a software developer who likes to poke around in security matters in as amateur a way as possible. The material covered here is a basic explanation, and there are many more factors in play. Feel free to [contact me](mailto:ireadeveryemail@fabisevi.ch) if you have more that you’d like to discuss.

**So, what’s the big deal?** 

Security is important. It should be bank’s top priority.

**Why does capitalization matter?** 

This lowers a hacker’s barrier to entry into your account by a factor of 26.

**How does this work?**

It’s simple enough. The total number of characters that you can enter will be called the *alphabet*.

> If you only allow lowercase letters, your total alphabet size is 26. (All the letters from a-z). 

> If you have lowercase and uppercase (A-Z), the size now doubles to 52.

> If you add in letters (0–9), now it is 62. 

> If you add in symbols (such as ?,!), your alphabet is now up to 95 characters, because there are 33 symbols on a standard keyboard. 

> Chase forbids you from using special symbols when creating a password, so you’re starting off with a maximum alphabet of 62 characters. 

We showed above that they are also not distinguishing between lowercase and capital letters, which lowers it again by 26 (since a is the same as A). That leaves us with a total of 36 characters to choose from to make a password. If you had the password `abcdefghij` (please don’t be this stupid) your password length is 10. You are only allowed to use 36 characters then the total number of possibilities is 36^10 total passwords. You can see this by splitting up the password. There are 36 options for the 1st character, 36 options for the 2nd, 36 for the 3rd and so on. If you were allowed to have an alphabet of 95 characters it becomes 95 options for the 1st, 95 for the 2nd, etc. 

How much safer is this? We’ll use the password `abcdefghij` for this mind experiment, and a set of computers that are making 100 billion guesses per second.

> If you had an alphabet of only lowercase numbers, it would take 24 minutes to crack that password through brute force.

> If you have an alphabet of lowercase and numbers, (Chase’s situation), the number jumps up to 10.45 hours. While this is a nice improvement, it is nothing that a little more CPU power can’t make into a problem. This really isn’t going to keep you safe for very long.

> If you have an alphabet where lowercase and uppercase numbers are different, along with numbers, the time to brute force jumps all the way up to 3.25 months. This is a vast improvement, but still is not something that a little horse power from a hacker can’t fix.

> An alphabet of lowercase, uppercase, numbers and symbols bumps that time up to 19.25 years. This is your gold standard. You should be changing your passwords more often than this as it is, and ideally passwords longer than 10 characters.

Most people don’t make their passwords complex or long, because they’re harder to remember. The price you pay with this approach is lack of security. That’s a price that you should not have to pay when dealing with your bank. It might cost you so much more than just your piece of mind. You can find out more information at [Steve Gibson’s Password Haystacks Page](https://www.grc.com/haystack.htm), and all the calculations are based on his search space calculator.