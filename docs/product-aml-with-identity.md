# AML Verification Combined with User Identification

<!-- theme: info -->
> #### TIP
> 
> The document describes how to verify the user and check the presence of his data on the AML lists. 
> Complements [Integration in 5 minutes](5minutesTutorial.md).

## Creating a Conversation

In order to retrieve information about the user's presence on the AML lists, a conversation must be created. 
Compared to the information contained in [Integration in 5 minutes](5minutesTutorial.md), we need to define an 
additional product for which we are asking: `aml`. It is also necessary to specify which lists should be checked. Example:

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
            "checks": ["PEP", "SANCTIONS", "ADVERSE_MEDIA", "SIP", "OTHER"]
        }
    }
}'
```

In the example above, we have set conversation to check the following lists:

- `PEP` - List of persons in politically exposed positions
- `SANCTIONS` - List of individuals for whom sanctions have been implemented
- `SIP` - List of individuals with high risk, typically involved in criminal activities or suspicious activity has been found in the past. May have been involved in court proceedings, had previous criminal allegations, or been involved in financial crimes such as money laundering and terrorist financing.
- `ADVERSE_MEDIA` - List of publications related to a person.
- `OTHER` - List of individuals for whom other categories than `PEP`, `SIP`, `SANCTIONS` have been implemented e.g. `RCA`, `POI`, etc.

A conversation defined this way returns an additional section in response to a query about its status:

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
            "status":"IN_PROGRESS"
        }
    }
}
```

Information: `status` acts identically to the `identity` section.

When a conversation is completed, the AML product reports in the `found` field those lists in which the
current user was found. A detailed report can be obtained by using the dedicated API method described
in the next section.

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
            "found": ["PEP", "SANCTIONS", "ADVERSE_MEDIA", "SIP", "OTHER"]
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

## Downloading detailed information

Having information on which lists the user was found on, it is possible to download a detailed report containing the 
collected information, e.g.:

```shell
curl -u my_login "https://sandbox.authologic.com/api/conversations/c12c1adc-3ff0-4d32-b95c-c593135c903e/aml/PEP" \
-H "accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json"
```

Parameterizing the call of the above method with the name of the AML list 
`PEP`, `SANCTIONS`, `SIP`, `ADVERSE_MEDIA` we get the first page of results for a given list.

The response structure varies depending on the selected AML list. A detailed 
description of the response structure can be found in the [AML product details](api/GET_conversations_ID_aml.md)
section.

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com

