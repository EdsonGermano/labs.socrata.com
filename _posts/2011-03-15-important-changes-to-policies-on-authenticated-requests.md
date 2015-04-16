---
title: Important changes to policies on authenticated requests
layout: post
---

As a part of our ongoing commitment to constantly re-evaluating the security of our APIs, we've made some changes to the requirements for authenticated requests to the Socrata Open Data API.

Note that these changes only affect _authenticated_ requests, so the vast majority of API users are not affected. This change only affects data publishing clients that are making authenticated requests in order to modify data. It does not affect unauthenticated read-only request from users of the Socrata Open Data Consumer API.

The following rules must be followed for all authenticated requests:

1. You can continue to use Basic Auth, but we're requiring that all requests that modify data be made over HTTPS.
2. Authenticated requests are also now required to include an Application Token with every request.

You will also no longer be able to use cookie-based authentication, as this can lead to insecure practices.

Adding an application token to your requests is straightforward:

1. [Register for an app token for your application](/register). If you don't want information about your application to be public, you can make the application profile private.
2. Add your app token to your request using either the `app_token` parameter or using the `X-App-Token` HTTP header.

For more information, see the article on [API authentication](/authentication). You can also ask questions via the [Developer Forum](http://support.socrata.com/forums/344875-developers-forum).
