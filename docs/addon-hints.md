# Using Hints

<!-- theme: warning -->
> #### WARNING
> 
> THIS FEATURE HAS BEEN DISCONTINUED! This means that it may be removed in future versions.

Authologic API allows you to pass the `hints` field. This is a structure that specifies additional 
information that is used to optimize or configure a query.

## Configure a Query
At this point, you can use the `hints` field to pass an user’s email address and telephone number to 
the strategy that allows them to be verified. If the request contains the appropriate 
field (`PERSON_CONTACT_EMAIL` or `PERSON_CONTACT_PHONE`), the process will skip asking the user for a 
phone number or email address and will use the one entered in the hints field.

Example:

<!--
title: "Example of creating a conversation"
-->
```json
{
  "userKey": "7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
  "returnUrl": "https://authologic.com/tests/return/?conversation={conversationId}",
  "callbackUrl": "https://system.acme.test/private/identity/{conversationId}/callback",
  "strategy": "{strategy}",
  "query": {
    "identity": {
      "requireOneOf": [
        ["PERSON_CONTACT_EMAIL", "PERSON_CONTACT_PHONE"]
      ]
    }
  },
  "hints": {
    "uncertain": {
      "person": {
        "contact": {
          "email": "jan.kowalski@email.com",
          "phone": "+4811111111"
        }
      }
    }
  }
}
```

## Optimizing a query
The `hints` field can also be used to pass user data that you know is true (`hints.known`)
or which are not certain (`hints.uncertain`). In some cases, Authologic may use them, e.g. when there 
is uncertainty as to the value of a field in a scanned document.

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
