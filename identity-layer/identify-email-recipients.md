---
title: Identify Email Recipients
description: This guide helps ensure your email recipients will be identified in Koala
---

# Identify Email Recipients

Koala is able to detect when a user clicks a link to your website from an outbound or marketing email. You can use this feature to collect identities from any clicks to your outreach messages.

This integration often leads to a boost of 20\~30% net new identities to your Koala workspace, allowing you to understand how your email prospects are interacting with your content and product.

Koala will also report all UTMs that drove the user to interact with your website from an email.

### Outreach.io

Koala offers an out of the box solution that allows you to track any clicks automatically. All links will be wrapped with a special param that is able to identify your users when they click any links from an Outreach message that points to your website.

You can install the [Koala Outreach Plugin](https://marketplace.outreach.io/apps/koala-id-links?store=unlisted) in the Outreach Marketplace. All links in your email will be automatically decorated with a `utm_id`.

Note: You need to be logged in to Outreach in order to be able to install the plugin from the App Marketplace. No further action required after you've installed the plugin.

### HubSpot

Koala offers HubSpot specific URL params that can be added to your Marketing and Sales email templates. Adding these URL params will enable you to track any clicks from when your Marketing or Sales Contacts click a link to your website.

#### Instructions:

1. Open the email template editor:
   * 1.a) For Sales templates: Select Conversations, then Templates
   * 1.b) For Marketing templates: Select Marketing, then Emails
2. Copy one of the following UTM Links:

If there are no other URL params

```
?ko_e={{contact.email}}&k_is=hs
```

If there are other URL params

```
&ko_e={{contact.email}}&k_is=hs
```

3. Add the Koala UTMs to links in your templates: ![HubSpot](https://app.getkoala.com/images/koala\_utms/hubspot.jpeg)

_💡 Note: Koala UTMs also work with your snippets. We recommend creating a handful of snippets that you can use for one-off emails._

### HubSpot (using base64 emails and utm\_id)

You can choose to send emails using the `utm_id` parameter, as opposed to the `ko_e` param.

The main difference between the two is that `ko_e` takes an email address as is, and the `utm_id` takes a base64 representation of an email, which obfuscates the email field, as well as compacts the size of the URL for long emails.

You can use all the same steps above, but instead use a `{{contact.base64_email}}` property in your templates.

#### Instructions:

1. Create a `base64_email` property in your Contact Object Schema
2. Create a HubSpot Workflow with the following steps:
   * a) Set the enrollment trigger to:
     * `Email` is known
     * `Email` has been updated in the last 1 day
   * b) Add a custom code step with the following script:

```javascript
exports.main = async (event, callback) => {
  const email = event.inputFields['email'];

  let binary = Buffer.from(email);
  let base64Encoded = binary.toString("base64");

  callback({
    outputFields: {
      base64_email: base64Encoded
    }
  });
}
```

![HubSpot Workflow](../images/identity-layer/hubspot-workflow.jpg)

```
- c) Set the `base64_email` output variable to the contact `base64_email` property
```

3\. Update your templates to use the `{{contact.base64_email}}` template property in all links to your website.

### Apollo.io

Update your sequence templates to add Koala UTM IDs to your links.

#### Instructions:

1. Open the Sequences email template editor:
   * a) Select Engage, then Sequences
2. Copy one of the following UTM Links:

If there are no other URL params

```
?ko_e={{email}}&k_is=apl
```

If there are other URL params

```
&ko_e={{email}}&k_is=apl
```

3.  Add the Koala UTMs to links in your templates:&#x20;

    <figure><img src="https://app.getkoala.com/images/koala_utms/apollo.jpg" alt=""><figcaption></figcaption></figure>

_💡 Note: Koala UTMs also work with your snippets. We recommend creating a handful of snippets that you can use for one-off emails._

### Salesloft

Update your templates to add Koala UTM IDs to your links.

#### Instructions:

1. Open the email template editor:
   * a) As described in the docs here.
2. Copy one of the following UTM Links:

If there are no other URL params

```
?ko_e={{email}}&k_is=sl
```

If there are other URL params

```
&ko_e={{email}}&k_is=sl
```

_💡 Note: Koala UTMs also work with your snippets. We recommend creating a handful of snippets that you can use for one-off emails._

### Amplemarket

Update your sequence templates to add Koala UTM IDs to your links.

#### Instructions:

1. Open the Sequences email template editor.
2. For all high-volume sequences, you'll want to change your links to contain the following UTM parameters:

If there are no other URL params

```
?ko_e={{email}}&k_is=am
```

If there are other URL params

```
&ko_e={{email}}&k_is=am
```

3.  Add the Koala UTMs to links in your templates:&#x20;

    <figure><img src="../images/koala_utms/amplemarket.png" alt=""><figcaption></figcaption></figure>

### Koala Email Params

You can tag any outbound links on any platform using the Koala Email param. All you need to is add ko\_e or utm\_id to any URL you'd like to be tracked when a prospect clicks it:

1. Start with an email address

```
tido@getkoala.com
```

2. Choose one of two flavors:

* a) A simple `ko_e` email param:

If there are no other URL params

```
?ko_e=email@example.com&k_is=dir
```

If there are other URL params

```
&ko_e=email@example.com&k_is=dir
```

* b) Or use `utm_id` with a base64 email parameter:

```javascript
let binary = Buffer.from(email);
let base64Encoded = binary.toString("base64");
```

3. Construct your URL:

```
https://getkoala.com/docs?ko_e=netto@getkoala.com
```

or if using option b

```
https://getkoala.com/docs?utm_id=${base64Encoded}
```

_Note: Option b is recommended for use cases where you're generating your URLs with a programing environment where you can base64 emails into IDs_

### Adding extra identification traits

You can add additional traits to enrich the identification of your email recipients. Koala detects any URL param that follows the pattern `ko_trait_<property>` and includes it in the traits list.

1. Start with the list of tratis you want to include

```
{
  first_name: 'Netto',
  last_name: `Farah`
}
```

2. Build the URL params

If there are no other URL params

```
?ko_trait_first_name=Netto&ko_trait_last_name=Farah
```

If there are other URL params

```
&ko_trait_first_name=Netto&ko_trait_last_name=Farah
```

3. Construct your URL:

```
https://getkoala.com/docs?ko_trait_first_name=Netto&ko_trait_last_name=Farah
```
