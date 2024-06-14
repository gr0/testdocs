# Integration in 5 minutes: Basic information

<!-- theme: warning -->
> The purpose of this document is to describe the general principle of integration with Authologic.
> We assume knowledge of the information contained in the [Overview](overview.md) document.

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
> link: [here](swagger-ui.md), or any other tool, such as Postman or Insomnia.

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
```shell
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
```java
import com.authologic.client.api.*;

import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        Client client = ClientBuilder.builder("username", "password").sandbox().build();

        Conversation conversation = client.execute(
            Requests.
                createConversation().
                strategy("public:sandbox").
                callbackUrl("some_callback_url").
                addProduct(
                    new IdentityProductQueryBuilder(
                        Arrays.asList(
                            IdentityQueryField.PERSON_NAME_FIRSTNAME,
                            IdentityQueryField.PERSON_NAME_LASTNAME
                        )
                    ))
        ).get();
        
        System.out.println(conversation.getUrl());
    }
}
```
Of course, instead of `_my_login_` enter your login. You should be prompted for a password - at that point you should 
enter *the API key* (do not confuse it with the password to the customer panel).

For `_my_callback_url_here_`  you could use https://webhook.site/ to generate callback url which will be responsible for 
receiving user information from Authologic. Whether you will use webhook.site or other similar tool it is crucial 
that it will correctly receive http request since *it is required for the process of identification*.

Authologic requires you to provide the API version number by providing them as part of the expected document types. 
Therefore, in the query, we used the appropriate `Accept` and `Content-Type` headers, thanks to which the server will be 
able to choose the appropriate format and API version. We then passed the query content in JSON format using the following:
userKey:: specifies the user you want to check. Authologic remembers this field, returns its value, but Authologic doesn't use the value of this field. Place there the user ID which is used in your system, it will make it easier for you to associate the conversation with the user. You can also ignore this fields and the Authologic will generate it for you.

- `returnUrl` - address to which the user will be redirected by Authologic after verifying the identity. It may contain the fragment: `{conversationId}` - if it exists, it will be replaced with the conversation ID.
- `callbackUrl` - after process is completed, on this url we will send you user information or information that process has failed.
- `strategy` - information on how Authologic should perform the verification. This field is *optional*. If not specified, the system will use the default value. In our case, we used the `public:sandbox` strategy, which does not perform real verification, but allows you to select the result, which is convenient for implementation and integration tests. You can read more about the test strategy [here](public-sandbox.md).

<!-- theme: info -->
> #### TIP
>
> We set the default strategy together when setting up an account. If you need to change it, please contact us.

<!-- theme: info -->
> #### TIP
>
> A list of the available strategies assigned to your account can be found on the main page of the customer portal.

<!-- theme: info -->
> #### TIP
>
> The example given is for a test environment. If you perform these operations on the production site 
> at: [https://api.authologic.com/](https://api.authologic.com/) then the `public:sandbox` strategy is not available. 
> You can omit the `strategy` field to use the default strategy or use another one that we gave you the name of when 
> determining your needs. As a result, nothing bad will happen, but remember that the production environment requires 
> real data. The collected data will also be real.

- `query` - it is the query definition that contains the set of information we want to receive.
- `identity`-  is the name of the product we want to ask for data. `Identity` specifies identity recognition. You will learn about other methods later.
- `requireOneOf` - data you want to be specified.

For this tutorial we use very simple set of data, but you probably noticed unusual structure of  an array of arrays,
find why and more detailed explanation: [here](addon-mandatoryAndOptionalQueries.md),
full list of available fields: [here](api/userInfoFields.adoc).
