# Additional Validations of the Verification Process

Some strategies perform additional validations on user data.
It might be the useful information in case the user data is not valid.

Let's look at an example ended conversation:

[source, json, indent = 0, subs=attributes+]
<!--
title: "An example of a conversation snippet with identity validations performed on user data."
-->
```json
{
    "id":"c12c1adc-3ff0-4d32-b95c-c593135c903e",
    "userKey":"7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
    "url":"https://sandbox.authologic.com/c/c12c1adc-3ff0-4d32-b95c-c593135c903e",
    "status":"FINISHED",
    "result":{
        "identity":{
            "status":"FINISHED",
            "errors": [],
            "user":{
                "person":{
                    "ids":{
                        "nationalId": "02070803629"
                    },
                    "info":{
                        "nationality": "PL"
                    }
                }
            },
            "checks":[
                {
                    "name": "CONSISTENCY_CHECK",
                    "result": "FAILED",
                    "details": {
                        "field": "PERSON_IDS_NATIONAL_ID",
                        "reason": "FORMAT_ERROR"
                    }
                }
            ]
        }
    }
}
```

In the example, the `result.identity.checks` section is visible. This is a list of validations performed on user data. 
The following data may appear here:

- `name`: the name of the validator
- `result`: the result of the validation process. This field may contain one of the following values:
  - `ACCEPTED` - the validation was performed and the result is positive,
  - `FAILED` - the validation was performed and the result is negative,
  - `ERROR` - the validation was performed, but an unexpected error occurred
- `details`: - validation process details. Details may have different properties depending on the validator

## Available validators

Below is a list of currently available validators. Please note that the list of validators will be expanded over time.
Some validators do not present the result if the result is positive.

| Name                  | Description                                         | Details |
|-----------------------|-----------------------------------------------------| ------- |
| CONSISTENCY_CHECK     | Validates data returned in `result.identity.user`.  | _details_ properties: 

* `field` - the name of the validated field. Possible values:
- `PERSON_IDS_NATIONAL_ID` - social security number format
* `reason` - the reason for the negative result. Possible values:
- `FORMAT_ERROR` - the field format is incorrect 

Validation is not presented if the result is positive. |

| FACE_MATCH |
| Interactive process of comparing the user's face with a photo from an identity document. |
| _details_ properties:

* `matchFound` - information whether the face matches the photograph. Possible values:
- `true/false`
* `reason` - reason of negative check. Possible values:
- e.g. `Unable to perform photo validation.` |

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
