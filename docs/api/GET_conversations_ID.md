# API: Querying the Conversation Status

## Address
*GET /api/conversations/{conversationId}*

## Description
The method is used to get information about the current conversation status.

## Example of a Query
n/a

## Description of Query Parameters
n/a

## Example of a Reply

<!--
title: "Example of the response with conversation status"
-->
```json
{
    "id":"e0c0b3cc-8238-414f-9940-9f14bd1b8693",
    "userKey":"d5dbb8e0-192e-4bc6-972c-f7948409d10c",
    "url":"https://sandbox.authologic.com/c/c12c1adc-3ff0-4d32-b95c-c593135c903e",
    "status":"FINISHED",
    "result":{
        "identity":{
            "status":"FINISHED",
            "user":{
                "person":{
                    "name":{
                        "firstName":"Jan",
                        "lastName":"Smith"
                    }
                }
            },
            "checks": [
                {
                    "name": "CONSISTENCY_CHECK",
                    "result": "FAILED",
                    "details": {
                        "field": "PERSON_IDS_NATIONAL_ID",
                        "reason": "FORMAT_ERROR"
                    }
                }
            ]
        },
        "aml": {
            "status":"FINISHED",
            "found": ["PEP", "SANCTIONS", "ADVERSE_MEDIA", "SIP", "OTHER"],
            "subscription": {
                "active": true,
                "lastChanged": "2020-09-17T11:18:21.999Z"
            }
        },
        "verify": {
            "status":"FINISHED",
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
        },
        "bankTransactions":{
            "status":"FINISHED"
        },
        "auth": {
            "status": "FINISHED",
            "token": "d42115b0-58d3-4e9b-b970-12ca7de181c7",
            "challenge": "1e03cd33-484e-49f4-b8e1-b8d273f8e8af"
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

## Description of the contents of the reply
| Parameter | Example                                                                       | Description                                                                                                                                                                                                                                                                                |
|-----------|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id | e0c0b3cc-8238-414f-9940-9f14bd1b8693                                          | Conversation ID.                                                                                                                                                                                                                                                                           |
| userKey | 7dfb9ded-c38f-49ae-95e2-307283a0b1f6                                          | User ID on your system.                                                                                                                                                                                                                                                                    |
| url | https://sandbox.authologic.com/c/c12c1adc-3ff0-4d32-b95c-c593135c903e         | A unique web address to which the user should be redirected to verify his identity.                                                                                                                                                                                                        |
| status | FINISHED                                                                      | Conversation status: `CREATED` - ready conversation, `IN_PROGRESS` - query data being specified,  `PARTIAL` - at least one product from the query has data ready to receive or has ended, `FINISHED` - query is complete,  `CANCELED` - user aborted, `EXPIRED` - conversation expired     |
| result | -                                                                             | Structure describing the information found                                                                                                                                                                                                                                                 |
| result.identity | -                                                                             | Structure describing the result of the identity check                                                                                                                                                                                                                                      |
| result.identity.status |                                                                               | Identity validation effect: `IN_PROGRESS` - checks in progress, `FINISHED` - checks from query complete, `PARTIAL` - checks completed but only part of the data could be determined, `FAILED` - checks completed but no data could be determined.                                          |
| result.identity.user | (see example in `hints.known` from `/api/conversations`)                      | User information                                                                                                                                                                                                                                                                           |
| result.identity.errors | ["SCAN_DOCUMENT_NOT_DETECTED"]                                                | Information about the causes of errors. The content depends on the specific method of verification                                                                                                                                                                                         |
| result.identity.checks | (see examples in [additional validations documentation](../addon-checks.md).) | A list of additional validations performed on user data                                                                                                                                                                                                                                    |
| result.aml | -                                                                             | Structure describing the result of user checking on AML lists                                                                                                                                                                                                                              |
| result.aml.status |                                                                               | User checking effect. Same as the `result.identity.status` field                                                                                                                                                                                                                           |
| result.aml.found | ["PEP", "SANCTIONS", "ADVERSE_MEDIA", "SIP", "OTHER"]                         | A table informing about the AML lists on which user data was found.                                                                                                                                                                                                                        |
| result.aml.subscription | -                                                                             | Structure that informs that the AMLs to be checked are periodic                                                                                                                                                                                                                            |
| result.aml.subscription.active | true                                                                          | Structure that informs about active periodic AML checking                                                                                                                                                                                                                                  |
| result.aml.subscription.lastChanged | "2020-09-17T11:18:21.999Z"                                                    | Date when the user's information on the AMLs was last changed                                                                                                                                                                                                                              |
| result.verify | -                                                                             | Structure describing the result of comparing the data obtained from the identity verification process                                                                                                                                                                                      |
| result.verify.status |                                                                               | Identity validation effect: `IN_PROGRESS` - checks in progress, `FINISHED` - checks from query complete, `PARTIAL` - checks completed but only part of the data could be determined, `FAILED` - checks completed but no data could be determined.                                          |
| result.verify.reliability | 0.66667                                                                       | A number specifying the similarity of the data obtained from the identity check process to the data provided in the query, where `0` means different data and `1.0` means identical data. Due to the differences in the format, data recording the value can be any value between 0 and 1. |
| result.verify.details | -                                                                             | Details of the individual data comparison storing the name of the field being compared and a number indicating the similarity of the data.                                                                                                                                                 |
| result.auth | -                                                                             | Structure describing the result of user authentication                                                                                                                                                                                                                                     |
| result.auth.status |                                                                               | Authentication status: `IN_PROGRESS` - checks in progress, `FINISHED` - checks from query complete, `FAILED` - checks completed but no data could be determined.                                                                                                                            |
| result.auth.token | a7d5d522-5308-4ec9-9789-53b4ec6d47ae                                          | A unique user ID associated with a given login method. Going through the login process again with the given method will always return the same token.                                                                                                                                      |
| result.auth.challenge | 403ad98c-c5fd-4991-a365-12ec70a93932                                          | A unique equivalent of the user login associated with a given login method. Used in methods that cannot determine who is authenticating and need this information to run the process.                                                                                                      |
| result.bankTransactions | -                                                                             | Structure describing the result of downloading transactions                                                                                                                                                                                                                                |
| result.bankTransactions.status |                                                                               | Effect of downloading transactions. Same as the `result.identity.status`                                                                                                                                                                                                                   |
| info | -                                                                             | Optional information containing an array describing the data sources used in the conversation.                                                                                                                                                                                             |
| info.country | PL                                                                            | Selected/used country in ISO 3166-1 alpha-2 format                                                                                                                                                                                                                                         |
| method | PSD2                                                                          | Data source used specifying the verification method or data source used.                                                                                                                                                                                                                   |

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com

