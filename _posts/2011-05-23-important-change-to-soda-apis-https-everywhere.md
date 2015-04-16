--- 
title: "Important change to SODA APIs: HTTPS Everywhere"
layout: post
---

In the coming week, we will be enabling a new feature on all Socrata-powered data sites that we call "HTTPS Everywhere". This frequently-requested feature will change the behavior of our platform to use secure HTTPS connections, just like your bank uses, for all interactions rather than just for the login page. This means that not only will your login be secure, but your entire session will be protected against the possibility of having a malicious third party hijack your session credentials using a technique that has gained some notoriety recently in the news as "[sidejacking](http://en.wikipedia.org/wiki/Session_hijacking)". Sidejacking allows a malicious third party on the same network as you to steal your session information and masquerade as you without needing to steal your username and password. Many prominent companies such as Google and Facebook allow HTTPS everywhere as an option - we are going a step further by making this the default for all data sites.

For API users, this means that **all** interactions with the Socrata Open Data Consumer and Publisher APIs must be performed over secure HTTPS connections. Otherwise, everything will continue to operate the same.

We'll be rolling out this feature on May 27th at 5PM Pacific Time. If you have any questions, feel free to email us at [support@socrata.com](mailto:support@socrata.com) or comment below.