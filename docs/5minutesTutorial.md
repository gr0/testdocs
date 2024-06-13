= Integration in 5 minutes: Basic information

<!-- theme: warning -->
> The purpose of this document is to describe the general principle of integration with Authologic.
> We assume knowledge of the information contained in the [Overview](https://authologic.com) document.

## Passwords
You have received three passwords with your username:

* Password to log in to the developer portal
* API key that you will use when communicating with Authologic.
* The key that you will use to verify the data sent by Authologic with the callback mechanism

<!-- theme: info -->
> #### TIP
>
> We use the `curl` tool to show the API operation. 
> If you have not dealt with it, you can find a short guide on it [here](https://www.baeldung.com/curl-rest).
> Of course, there is nothing to prevent you from using the swagger tool directly, which you will find at the 
> link: [here](https://authologic.com), or any other tool, such as Postman or Insomnia.

## Creating a Conversation
So let's try using the `curl` tool to start a new conversation, which is the identity checking process.

<!-- theme: warning -->
> #### Warning!
>
> The conversation creation API does not have any mandatory fields. This is because your account
> may have default values for all fields configured. Thanks to this, possible changes in the requirements are not
> connected with your code.

The Authologic API uses the `Basic Auth` based authentication described, among others, at [here](https://en.wikipedia.org/wiki/Basic_access_authentication). 
Username and *API key* should be used as data. By using the `curl` tool we use the `-u` option which is responsible for the use of `Basic Auth`.

<!--
title: "Create Conversation"
highlightLines: [[5,13]]
-->
```
curl -X POST -u my_login "https://sandbox.authologic.com/api/conversations" \
-H "Accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json" \
-d '{
    "userKey": "7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
    "returnUrl": "https://authologic.com/tests/return/?conversation={conversationId}",
    "callbackUrl": "my_callback_url_here",
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
