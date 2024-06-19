# Monitoring AML Lists Changes

<!-- theme: info -->
> #### TIP
> 
> Document describes how to track AML changes in the context of a specific user. 
> It complements [AML Verification](product-aml.md).

## Create a Conversation
The [AML Verification](product-aml.md) document describes how to create a user verification that includes
one-time check of AML lists. We will modify the example of setting up a conversation given there so that Authologic 
informs you us about any changes to the given AML lists related to this user:

```shell
curl -X POST -u my_login "https://sandbox.authologic.com/api/conversations" \
-H "accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json" \
-d '{
  "userKey": "7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
  "returnUrl": "https://authologic.com/tests/return/?conversation={conversationId}",
  "query": {
    "identity": {
      "requireOneOf": [
        [ "PERSON_NAME_FIRSTNAME", "PERSON_NAME_LASTNAME"]
      ]
    },
    "aml": {
      "checks": ["PEP", "SANCTIONS", "ADVERSE_MEDIA", "SIP", "OTHER"],
      "subscription": {}
    }
  }
}'
```

The difference in the query is adding the fragment: `"subscription": {}`. The answer is automatically expanded
for subscription status, e.g .:

```json
{
    "id":"c12c1adc-3ff0-4d32-b95c-c593135c903e",
    "userKey":"7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
    "url":"https://sandbox.authologic.com/c/c12c1adc-3ff0-4d32-b95c-c593135c903e",
    "status":"CREATED",
    "result":{
        "identity":{
            "status":"IN_PROGRESS",
            "user":{}
        },
        "aml": {
            "status":"IN_PROGRESS",
            "subscription": {
              "active": true
            }
        }
    }
}
```

After the first check, there will also be an additional `lastChanged` field containing the date the last content change was detected
AML lists provided in the query.

```json
{
    "id": "c12c1adc-3ff0-4d32-b95c-c593135c903e",
    "userKey":"7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
    "url":"https://sandbox.authologic.com/c/c12c1adc-3ff0-4d32-b95c-c593135c903e",
    "status": "FINISHED",
    "result": {
        "identity": {
            "status": "FINISHED",
            "user": {
                "person": {
                    "name": {
                        "firstName": "Maria",
                        "lastName": "Sochacka"
                    }
                }
            }
        },
        "aml": {
            "status": "FINISHED",
            "found": ["PEP", "SANCTIONS", "ADVERSE_MEDIA", "SIP", "OTHER"],
            "subscription": {
                "active": true,
                "lastChanged": "2022-08-12T13:42:53.018798Z"
            }
        }
    },
    "info": [
        {
            "country": "PL",
            "method": "PSD2"
        }
    ]
}
```

## Information About Changes
After detecting changes in monitored AML lists, Authologic automatically sends information about it via the callback mechanism,
where `target` = `SUBSCRIPTION` and `event` = `NEW_DATA`. The general structure of callbacks is described in
[Using change notifications](callback.md).

## Subscription Cancellation

Authlogic performs AML monitoring until the subscription is canceled. This continues until the
`DELETE /api/subscriptions/{conversationId}/aml` method call. After successful unsubscription, 
the system responds with a header HTTP: `204 No Content`.

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
