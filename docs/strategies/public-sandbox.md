# Test strategy `public: sandbox`

## Name
*public:sandbox*

## Supported products
- `identity` - identity verification
- `verify` - comparison with provided data

## Description
When creating the integration and pre-testing it is more convenient to use the test as the method of verification. 
To do this, when creating a conversation, you must force a different verification strategy as follows:

```shell
curl -X POST -u my_login "https://sandbox.authologic.com/api/conversations" \
-H "accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json" \
-d '{
	"userKey": "7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
	"returnUrl": "https://authologic.com/tests/return/?conversation={conversationId}",
	"strategy": "public:sandbox",
	"query": {
		"identity": {
			"requireOneOf": [
				[ "PERSON_NAME_FIRSTNAME", "PERSON_NAME_LASTNAME"]
			]
		}
	}
}'
```

The conversation created differs from the real one with the following elements:

- This way all unnecessary screens are omitted, e.g. collecting consents
- The user can enter the required data by himself, thus triggering different verification results
- Allows you to specify whether the data is to be sent with the `callback` mechanism before returning to your website, or with a delay, which allows you to simulate both synchronous and asynchronous strategies. 
- The entered data is saved, so the next use of the strategy is faster, which is not without significance when working on the integration and later testing it.

## Supported user fields
No restrictions

## Parameters
n/a

## Action
n/a

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
