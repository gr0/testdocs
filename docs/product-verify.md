# Comparison of the Verification Data and the Data Which You Provided

<!-- theme: info -->
> #### TIP
> 
> This document describes how to use Authologic to compare the downloaded data. 
> Complements [5 Minutes Integration](5minutesTutorial.md).

## Creating a Conversation

Data Validation is an additional product that can be added when creating a conversation. Compared to the information contained
in [5 Minutes Integration](5minutesTutorial.md) we need to define an additional section: `verify`, containing the data to be verified 
by the system.

Example:

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
        "verify": {
            "user": {
                "person": {
                    "name": {
                        "firstName": "Jon",
                        "lastName": "Testowy"
                    }
                }
            }
        }
    }
}'
```

The transaction defined this way, in response to its status, has an additional section:

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
        "verify": {
            "status":"IN_PROGRESS"
        }
    }
}
```

Note: `status` behaves identically to the `identity` section.

## End of conversation

After the end of the conversation, information about the result of the comparison is displayed in the section containing 
the result of the action:

```json
{
  "id":"c12c1adc-3ff0-4d32-b95c-c593135c903e",
  "userKey":"7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
  "url":"https://sandbox.authologic.com/c/c12c1adc-3ff0-4d32-b95c-c593135c903e",
  "status": "FINISHED",
  "result": {
      "identity": {
          "status": "FINISHED",
          "user": {
              "person": {
                  "name": {
                      "firstName": "Jan",
                      "lastName": "Testowy"
                  }
              }
          }
      },
      "verify": {
          "status": "FINISHED",
          "reliability": 0.6666666666666667,
          "details": [
              {
                  "field": "PERSON_NAME_FIRSTNAME",
                  "reliability": 0.6666666666666667
              },
              {
                  "field": "PERSON_NAME_LASTNAME",
                  "reliability": 1
              }
          ]
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

As you can see in the example, the answer contains a numeric measure of the fit of the data, on a scale of 0 (other data) to 1 (100% match).
It also includes a comparison for each field separately.

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
