---
title: Identifying Users
description: >-
  Koala provides several ways to identify or deanonymize your visitors. We'll
  discuss the two most common ways we deanonymize your visitors, and then answer
  some frequently asked questions about the top
hidden: true
---

# Identifying Users

#### IP to Company matching

Koala partners with Clearbit to power IP to company intelligence using the Clearbit Reveal product.

If you are already a Clearbit Reveal customer, you can simply connect Koala to your Clearbit account using your Clearbit API key.

If you don't yet use Clearbit Reveal, you can provision a Clearbit key through Koala that includes up to 10,000 Reveal calls per month and 2,500 Enrich calls per month, with pay-as-you-go plans if you need more.

Manage your Clearbit integration from the [Clearbit settings page](https://app.getkoala.com/goto/apps/clearbit).

#### IP Geocoding

Koala also provides IP-based geolocation to give you a better idea of where your visitors are from. This is especially helpful when you have an anonymous visitor from an account and can use the city/state/country and another tool like Sales Navigator to figure out who it is.

#### First-party identification

When users do something identifiable in your app, like logging in or registering an account, you can identify them manually. This enables you to:

* Track a visitor across browsers or devices
* Differentiate truly anonymous visitors from known users
* Combine all activity from a visitor before and after they've logged in Associate visitors with company data

The most effective way to do first-party identification is to instrument a `ko.identify(email)` call using the [client-side SDK](get-started/quick-start/).

If you're using Segment, Koala will automatically detect and forward \`identify\` calls from Segment's analytics.js library to \`ko.identify\` by default (unless you've explicitly disabled it).

Koala also automatically collects non-sensitive form submissions, like your demo request form, webinar registration, or content download forms. Our client-side SDK combines several hueristics to collect email and other user traits from form submissions.

### FAQ

Similar to other analytics tools, the same device and browser is considered to be the same visitor. When someone logs out, we recommend you call \`ko.reset()\` to reset the identify tied to that browser. Koala automatically detects form inputs and ignores sensitive fields. If there are visitor or account traits you want to capture, you can manually instrument that via \`ko.identify\` though (client-side or server-side)! Yes! Koala automatically handles all of that identify merging logic. If it is an anonymous session, Koala will associate that session with the email given in the form-fill. However, Koala prioritizes \`ko.identify\` calls, so if there is a login and accompanying \`ko.identify\` call, it will be overridden with the data from the login.
