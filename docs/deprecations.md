# Unsupported and Deprecated Functions

Information about functionalities that will be removed and may require updating your system.

## Changes in Handling of Hints Functionality 

The following section describes the changes in the `hints` functionality and adding new fields, the
`PERSON_CONTACT_EMAIL_OTP` and `PERSON_CONTACT_PHONE_OTP` along with changing in handling of the
`PERSON_CONTACT_EMAIL` and `PERSON_CONTACT_PHONE` fields.

### End of Support Date: 1/8/2024

### Changes in Hints Support

The functionality that allows checking if user's email or phone number is correct via hints is moved to the settings section.
Query implementing this functionality:

```json
  ...
  "query": {
    "identity": {
      "requireOneOf": [
        [
          "PERSON_CONTACT_EMAIL",
          "PERSON_CONTACT_PHONE"
        ]
      ]
    }
  },
    "hints": {
    "uncertain": {
      "person": {
        "contact": {
          "email": "uncertain@email.com",
          "phone": "+48123123123"
        }
      }
    }
  },
  ...
}
```

should be replaced with:

```json
{
  ...
  "query": {
    "identity": {
      "requireOneOf": [
        [
          "PERSON_CONTACT_EMAIL_OTP",
          "PERSON_CONTACT_PHONE_OTP"
        ]
      ]
    }
  },
  "settings": {
    "personContactEmailForOTP": "uncertain@email.com",
    "personContactPhoneForOTP": "+48123123123"
  }
  ...
}
```

The new query uses the fields `PERSON_CONTACT_EMAIL_OTP`, `PERSON_CONTACT_PHONE_OTP` and 
will return data in the `emailOtp` or `phoneOtp` fields.

### New fields PERSON_CONTACT_EMAIL_OTP, PERSON_CONTACT_PHONE_OTP

When creating a conversation, you can ask for the user's contact details. The user verifies the 
authenticity of his email or telephone number with a one-time code. To do this, you had to add an 
appropriate field to the query section, e.g.:

```json
...
 "query": {
    "identity": {
      "requireOneOf": [
        [
          "PERSON_CONTACT_EMAIL"
        ]
      ]
    }
  }
}
...
```

Currently, the equivalent of this query will be:

```json
...
  "query": {
     "identity": {
       "requireOneOf": [
         [
           "PERSON_CONTACT_EMAIL_OTP"
         ]
       ]
     }
   }
}
...
```

In the response, the `email` field will be replaced with the `emailOtp` field. For example, 
a following callback would be sent to the above query:

```json
{
  "id": "3f8263f2-b014-474e-ac17-0783474e9df0",
  "created": "2024-04-18T13:28:26.078570025+02:00",
  "target": "CONVERSATION",
  "event": "FINISHED",
  "payload": {
    "conversation": {
      "id": "9fcfdda4-30b8-4e80-bcd6-7dd4c9633dc7",
      "userKey": "userKey",
      "url": "url",
      "status": "FINISHED",
      "result": {
        "identity": {
          "status": "FINISHED",
          "errors": [],
          "user": {
            "person": {
              "contact": {
                "emailOtp": "example@email.com"
              }
            }
          }
        }
      }
    }
  }
}
```

### Backwards compatibility

Until the end of the support period, the `PERSON_CONTACT_EMAIL`, `PERSON_CONTACT_PHONE` fields (unless they are 
combined with the `PERSON_CONTACT_EMAIL_OTP`, `PERSON_CONTACT_PHONE_OTP` fields) will work in the same way as before.

### Combining fields

If both types of fields appear in the query, e.g.:

```json
...
  "query": {
     "identity": {
       "requireOneOf": [
         [
           "PERSON_CONTACT_EMAIL",
           "PERSON_CONTACT_EMAIL_OTP"
         ]
       ]
     }
   }
}
...
```

the system will first ask the data provider for the email field (if the provider provides such information), 
and then will display to the user a form asking for email verification with a one-time code, the `email` 
and `emailOtp` fields will be sent in response, with the `email` field containing the data coming from the 
supplier, and `emailOtp` data confirmed with a one-time code. Sample answer:

```json
...
       "result": {
         "identity": {
           "status": "FINISHED",
           "errors": [],
           "user": {
             "person": {
               "contact": {
                 "email": "example_mail@email.com"
                 "emailOtp": "another_mail@email.com"
               }
             }
           }
         }
       }
...
```

### Exceptions

Since the `public:mi` strategy received data directly from the provider and did not verify it through the 
one-time code mechanism, there is no need for migration for this strategy.

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com

