# Use of Mandatory And Optional Queries

When creating a conversation, it is necessary to provide user fields that the verification should fill in.
These fields are divided into:

- `requireOneOf`: here you enter the sets of the fields that you have specified as required for the verification to be successful. Think of these sections as "require one of defined sets". In the example below, it is required to provide on of 2 sets of data.
- `optional`: here you specify the fields that will be returned if successfully determined in the verification process. Their absence does not affect the final result of the verification.

Please note how the `requireOneOf` and `optional` fields are structured. The former is an array of arrays, which allows to define
several equivalent data sets that the identity verification should return. For example:

```json
"requireOneOf": [
  [
    "PERSON_NAME_FIRSTNAME",
    "PERSON_NAME_LASTNAME",
    "PERSON_IDS_NATIONAL_ID"
  ],
  [
    "PERSON_NAME_FIRSTNAME",
    "PERSON_NAME_LASTNAME",
    "PERSON_IDS_PASSPORT_ID"
  ]
]
```

means that the verification is successful if the name and surname of the user as well as their national number
or passport number have been identified.

In the case of the `optional` field, the structure is a list of objects containing the `list` field. This field 
specifies those fields that do not have to be returned by conversation, unless they were directly available from 
the identity provider. In practice, it is enough to provide only one object. In the future, this structure may be expanded to 
include more complex cases.

After the verification is completed, Authologic will set the appropriate value of the `result.identity.status` field:
- `FINISHED` - if it was possible to define of all the fields in any set,
- `PARTIAL` - if it was possible to define only some fields,
- `FAILED` - if no field has been specified.

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
