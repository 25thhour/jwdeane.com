---
title: Unable to set HSTS header in Cloudflare Pages _headers file
description: Setting the Strict-Transport-Security header in a Cloudflare Pages _headers file is ignored at build time.
date: 2022-01-17
tags:
  - cloudflare
  - cf-pages
layout: layouts/post.njk
---

When trying to set the `Strict-Transport-Security` header in this sites [`_headers` file](https://github.com/25thhour/jwdeane.com/commit/03783a46ecc968f9de989b2f15e7939febaebe02#diff-36d2e18f82e5a1b5840515b6b51620fa614e3863b5767a9f5c7634843216e7d3R10) I noticed that it was ignored when redeploying the site.

```
/*
  X-Frame-Options: DENY
  X-Content-Type-Options: nosniff
  Referrer-Policy: no-referrer
  Permissions-Policy: document-domain=()
  Content-Security-Policy: script-src 'self' https://static.cloudflareinsights.com/beacon.min.js; frame-ancestors 'none';
  Strict-Transport-Security: max-age=1000; includeSubDomains
```

:thinking: This _may_ be due to Cloudflare requiring HSTS to be set via the [Origin SSL HSTS configuration](https://developers.cloudflare.com/ssl/edge-certificates/additional-options/http-strict-transport-security).

Adding these headers in the first place was inspired by Scott Helme's [blog post](https://scotthelme.co.uk/security-headers-cloudflare-worker/) and the Cloudflare Pages docs on [security hardening](https://developers.cloudflare.com/pages/platform/headers#harden-security-for-an-application).
