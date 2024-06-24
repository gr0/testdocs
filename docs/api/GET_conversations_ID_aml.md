# API: Query for Data Aggregated on AML Lists

## Address
*GET /api/conversations/{conversationId}/aml/{list}*

## Description
The method retrieves data found in AML lists based on user data.
Data from AML lists as defined when creating the conversation.

When a continuous AML monitoring subscription is activated, only the latest available data is returned.

## Query example
We can specify the list type in the query by specifying one of the following AML list 
types: `PEP`, `SIP`, `SANCTIONS`, `ADVERSE_MEDIA`, `OTHER`.

<!--
title: "Example request for PEP list data"
-->
```shell
curl -u my_login "https://sandbox.authologic.com/api/conversations/c12c1adc-3ff0-4d32-b95c-c593135c903e/aml/PEP" \
-H "accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json"
```

## Query Parameters Description
The method supports the following query parameters:

| Parameter | Example | Description |
| --------- | ------- | ----------- |
| page | 10 | Page number. Paging starts on page 0 (default). |
| pageSize | 10 | Number of transactions on the results page. Currently, values above 200 are treated as 200. |

## Response Example
Depending on the type of list you select, the structure of the response may vary.

- [Response including `PEP` list data](GET_conversations_ID_aml__pep_response_example.md)
- [Response including `SANCTIONS` list data](GET_conversations_ID_aml__sanctions_response_example.md)
- [Response including `SIP` list data](GET_conversations_ID_aml__sip_response_example.md)
- [Response including `ADVERSE_MEDIA` list data](GET_conversations_ID_aml__adverse_media_response_example.md)
- [Response including `OTHER` list data](GET_conversations_ID_aml__other_response_example.md)

The key message for all responses is: `more` parameter. If it has the value: `true`, then we can query the next page of results by adding
parameter to the query: `page`:

<!--
title: "Example of retrieving data from a PEP list with a results page number"
-->
```shell
curl -u my_login "https://sandbox.authologic.com/api/conversations/c12c1adc-3ff0-4d32-b95c-c593135c903e/aml/PEP?page=1" \
-H "accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json"
```

By modifying the parameter: `page`, we can retrieve subsequent pages of results until the response shows `more` set to `false`.

## Response content

A detailed description of the fields returned depending on the type of AML list.

<!-- theme: info -->
> #### TIP
>
> AML verification sources provide data in an inconsistent form, e.g., some dates and country names.
> We currently provide this data as received from the source, but in future we may unify them on Authologic side.
> This may change the format of the data available to the API.

### Response parameters available for PEP list

| Parameter                              | Example                                 | Description                                                                              |
|----------------------------------------|-----------------------------------------|------------------------------------------------------------------------------------------|
| type                                   | PERSON                                  | Informs if entry describes user or users's relative: `PERSON` - user, `RCA` - users's relative |
| score                                  | 0.98                                    | Compliance level of provided personal data with results (0-1 if provided or null)        |
| reason                                 | --                                      | Reason why person is on the list                                                         |
| user.person                            | --                                      | Data found on AML lists for provided person                                              |
| user.person.name.firstName             | --                                      | User name                                                                                |
| user.person.name.lastName              | --                                      | User surname                                                                             |
| user.person.name.middleName            | --                                      | Second name                                                                              |
| user.person.name.spellings             | --                                      | Correct spelling of name and surname (including national language)                       |
| user.person.name.alsoKnownAs           | --                                      | Alias names of person under verification                                                 |
| user.person.name.alsoKnownAs.firstName | --                                      | User's other firstname                                                                   |
| user.person.name.alsoKnownAs.lastName  | --                                      | User's other surname                                                                     |
| user.person.name.alsoKnownAs.title     | --                                      | User alias                                                                               |
| user.person.address.country            | POLAND (no unified country name format) | Country of residence of the person                       |
| user.person.info                       | --                                      | Additional information about the person under verification                               |
| user.person.info.gender                | MALE                                    | The gender of the user: `MALE`, `FEMALE`, `OTHER`                                        |
| user.person.info.nationality           | Poland (no unified country name format) | User's nationality                                       |
| user.person.info.birthDate             | 1972-10-18 (no unified date format)     | Date of birth |
| user.person.info.deceased              | true/false                              | Information if person is dead |
| user.person.info.deceaseDate           | 2020-10-18 (no unified date format)     | Date of death |
| user.person.info.image                 | --                                      | URL to person's picture |
| user.person.info.roles                 | --                                      | Information about the exposed position held by the person |
| user.person.info.roles[].title         | --                                      | Position held or `Unknown` if position is unknown |
| user.person.info.roles[].country       | (no unified country name format)        | The country in which the position was held or 'Unknown' if country is unknown |
| user.person.info.roles[].fromDate      | 2014-05-01 (no unified date format)     | Start date of tenure |
| user.person.info.roles[].tillDate      | 2019 (no unified date format)           | End date of tenure |

### Response parameters available for SANCTIONS list
| Parameter                                           | Example | Description                                                                                   |
|-----------------------------------------------------|---------|-----------------------------------------------------------------------------------------------|
| type                                                | PERSON  | Informs if entry describes user or users's relative: `PERSON` - user, `RCA` - user's relative |
| score | 0.98 | Compliance level of provided personal data with results (0-1 if provided or null) |
| reason | -- | Reason why person is on the list |
| sources | -- | Names of AML list types on which the person was found |
| user.person | -- | Data found on AML lists for provided person |
| user.person.name.firstName | -- | User name |
| user.person.name.lastName | -- | User surname |
| user.person.name.middleName | -- | Second name |
| user.person.name.spellings | -- | Correct spelling of name and surname (including national language) |
| user.person.name.alsoKnownAs | -- | Alias names of person under verification |
| user.person.name.alsoKnownAs.firstName | -- | User's other firstname |
| user.person.name.alsoKnownAs.lastName | -- | User's other surname |
| user.person.name.alsoKnownAs.title | -- | User alias |
| user.person.address.country | POLAND (no unified country name format) | Country of residence of the person |
| user.person.info | -- | Additional information about the person under verification |
| user.person.info.gender | MALE | The gender of the user: `MALE`, `FEMALE`, `OTHER` |
| user.person.info.nationality | Poland (no unified country name format) | User's nationality |
| user.person.info.birthDate | 1972-10-18 (no unified date format) | Date of birth |
| user.person.info.deceased | true/false | Information if person is dead |
| user.person.info.deceaseDate | 2020-10-18 (no unified date format)| Date of death |
| user.person.info.image | -- | URL to person's picture |
| user.person.info.roles | -- | Information about the exposed position held by the person |
| user.person.info.roles[].title | -- | Position held or 'Unknown' if position is unknown |
| user.person.info.roles[].country | (no unified country name format) | The country in which the position was held or 'Unknown' if country is unknown |
| user.person.info.roles[].fromDate | 2014-05-01 (no unified date format) | Start date of tenure |
| user.person.info.roles[].tillDate | 2019 (no unified date format) | End date of tenure |

### Response parameters available for SIP list
| Parameter | Example | Description                                                                                  |
|-----------| ------- |----------------------------------------------------------------------------------------------|
| type      | PERSON    | Informs if entry describes user or users's relative `PERSON` - user, `RCA` - user's relative |
| score | 0.98 | Compliance level of provided personal data with results (0-1 if provided or null) |
| reason | -- | Reason why person is on the list |
| user.person | -- | Data found on AML lists for provided person |
| user.person.name.firstName | -- | User name |
| user.person.name.lastName | -- | User surname |
| user.person.name.middleName | -- | Second name |
| user.person.name.spellings | -- | Correct spelling of name and surname (including national language) |
| user.person.name.alsoKnownAs | -- | Alias names of person under verification |
| user.person.name.alsoKnownAs.firstName | -- | User's other firstname |
| user.person.name.alsoKnownAs.lastName | -- | User's other surname |
| user.person.name.alsoKnownAs.title | -- | User alias |
| user.person.address.country | POLAND (no unified country name format) | Country of residence of the person |
| user.person.info | -- | Additional information about the person under verification |
| user.person.info.gender | `MALE` | The gender of the user: `MALE`, `FEMALE`, `OTHER`  |
| user.person.info.nationality | Poland (no unified country name format) | User's nationality |
| user.person.info.birthDate | 1972-10-18 (no unified date format) | Date of birth |
| user.person.info.deceased | true/false | Information if person is dead |
| user.person.info.deceaseDate | 2020-10-18 (no unified date format) | Date of death |
| user.person.info.image | -- | URL to person's picture |
| user.person.info.roles | -- | Information about the exposed position held by the person |
| user.person.info.roles[].title | -- | Position held or 'Unknown' if position is unknown |
| user.person.info.roles[].country | (no unified country name format) | The country in which the position was held or `Unknown` if country is unknown |
| user.person.info.roles[].fromDate | 2014-05-01 (no unified date format) | Start date of tenure |
| user.person.info.roles[].tillDate | 2019 (no unified date format) | End date of tenure |

### Response parameters available for ADVERSE_MEDIA list
| Parameter | Example | Description |
| --------- | ------- | ----------- |
| originalUrl | -- | Link to adverse article |
| date | 2020-10-18 (date format yyyy-MM-dd) | Adverse media publication date |
| url | -- | Link to PDF with original adverse media publication |
| categories | -- | Media categorization |

### Response parameters available for `OTHER list
| Parameter | Example | Description |
|-----------| ------- | ----------- |
| type | PERSON    | Informs if entry describes user or users's relative: `PERSON` - user, `RCA` - user's relative |
| score | 0.98 | Compliance level of provided personal data with results (0-1 if provided or null) |
| reason | -- | Reason why person is on the list |
| user.person | -- | Data found on AML lists for provided person |
| user.person.name.firstName | -- | User name |
| user.person.name.lastName | -- | User surname |
| user.person.name.middleName | -- | Second name |
| user.person.name.spellings | -- | Correct spelling of name and surname (including national language) |
| user.person.name.alsoKnownAs | -- | Alias names of person under verification |
| user.person.name.alsoKnownAs.firstName | -- | User's other firstname |
| user.person.name.alsoKnownAs.lastName | -- | User's other surname |
| user.person.name.alsoKnownAs.title | -- | User alias |
| user.person.address.country | POLAND (no unified country name format) | Country of residence of the person |
| user.person.info | -- | Additional information about the person under verification |
| user.person.info.gender | MALE | The gender of the user: `MALE`, `FEMALE`, `OTHER` |
| user.person.info.nationality | Poland (no unified country name format) | User's nationality |
| user.person.info.birthDate | 1972-10-18 (no unified date format) | Date of birth |
| user.person.info.deceased | true/false | Information if person is dead |
| user.person.info.deceaseDate | 2020-10-18 (no unified date format) | Date of death |
| user.person.info.image | -- | URL to person's picture |
| user.person.info.roles | -- | Information about the exposed position held by the person |
| user.person.info.roles[].title | -- | Position held or `Unknown` if position is unknown |
| user.person.info.roles[].country | (no unified country name format) | The country in which the position was held or `Unknown` if country is unknown |
| user.person.info.roles[].fromDate | 2014-05-01 (no unified date format) | Start date of tenure |
| user.person.info.roles[].tillDate | 2019 (no unified date format) | End date of tenure |

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
