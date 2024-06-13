= Integration in 5 minutes: Basic information

:memo: The purpose of this document is to describe the general principle of integration with Authologic. We assume knowledge of the information contained in the xref:overview.adoc[Overview] document.

== Passwords
You have received three passwords with your username:

* Password to log in to the developer portal
* API key that you will use when communicating with Authologic.
* The key that you will use to verify the data sent by Authologic with the callback mechanism


:bulb: **TIP**: We use the `curl` tool to show the API operation. If you have not dealt with it, you can find a short guide on it [here](https://www.baeldung.com/curl-rest).
Of course, there is nothing to prevent you from using the swagger tool directly, which you will find at the link: link:/api-docs/swagger-ui/index.html[here^], or any other tool, such as Postman or Insomnia.

== Creating a Conversation
So let's try using the `curl` tool to start a new conversation, which is the identity checking process.

:warning: **WARNING** The conversation creation API does not have any mandatory fields. This is because your account
may have default values for all fields configured. Thanks to this, possible changes in the requirements are not
connected with your code.

The Authologic API uses the `Basic Auth` based authentication described, among others, at [here](https://en.wikipedia.org/wiki/Basic_access_authentication). 
Username and *API key* should be used as data. By using the `curl` tool we use the `-u` option which is responsible for the use of `Basic Auth`.

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

Of course, instead of `_my_login_` enter your login. You should be prompted for a password - at that point you should enter *the API key* (do not confuse it with the password to the customer panel).

For
`_my_callback_url_here_`  you could use https://webhook.site/ to generate callback url which will be responsible for receiving user information from Authologic. Whether you will use webhook.site or other similar tool it is crucial that it will correctly receive http request since *it is required for the process of identification*.

Authologic requires you to provide the API version number by providing them as part of the expected document types. Therefore, in the query, we used the appropriate `Accept` and `Content-Type` headers, thanks to which the server will be able to choose the appropriate format and API version. We then passed the query content in JSON format using the following:

userKey:: specifies the user you want to check. Authologic remembers this field, returns its value, but Authologic doesn't use the value of this field. Place there the user ID which is used in your system, it will make it easier for you to associate the conversation with the user. You can also ignore this fields and the Authologic will generate it for you.

returnUrl:: address to which the user will be redirected by Authologic after verifying the identity. It may contain the
fragment: `{conversationId}` - if it exists, it will be replaced with the conversation ID.

callbackUrl::  after process is completed, on this url we will send you user information or information that proces has failed.

strategy:: information on how Authologic should perform the verification. This field is *optional*. If not specified, the system will use the default value. In our case, we used the `public:sandbox` strategy, which does not perform real verification, but allows you to select the result, which is convenient for implementation and integration tests. You can read more about the test strategy xref:strategies/public-sandbox.adoc[here].

TIP: We set the default strategy together when setting up an account. If you need to change it, please contact us.

TIP: A list of the available strategies assigned to your account can be found on the main page of the customer portal.

TIP: The example given is for a test environment. If you perform these operations on the production site at: https://api.authologic.com/[^] then the `public:sandbox` strategy is not available. You can omit the `strategy` field to use the default strategy or use another one that we gave you the name of when determining your needs. As a result, nothing bad will happen, but remember that the production environment requires real data. The collected data will also be real. icon:smile-o[]

query:: it is the query definition that contains the set of information we want to receive.

identity:: is the name of the product we want to ask for data. `Identity` specifies identity recognition. You will learn about other methods later.

requireOneOf:: data you want to be specified.
For this tutorial we use very simple set of data, but you probably noticed unusual structure of  an array of arrays,
find why and more detailed explanation: xref:addon-mandatoryAndOptionalQueries.adoc[here],
full list of available fields: xref:api/userInfoFields.adoc[here]

The response should look something like this:
[source,json,indent=0]
.Reply: Conversation created
----
    {
        "id":"c12c1adc-3ff0-4d32-b95c-c593135c903e",
        "userKey":"7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
        "url":"https://sandbox.authologic.com/c/c12c1adc-3ff0-4d32-b95c-c593135c903e",
        "status":"CREATED",
        "result":{
            "identity":{
                "status":"IN_PROGRESS",
                "user":{}
            }
        }
    }
----

We got the following information here:

id::  it is the conversation id. We will need it when inquiring about its status.

userKey:: ID of the user to be checked, exactly what you entered when creating the conversation.

url:: the address to which the user should be redirected in order to verify the identity.

status:: conversation status. `_CREATED_` marks a new conversation where the user has not yet started the verification process.

result:: conversation result. At the moment we do not have any data, so there appears, within the product
for which we asked the status: `_IN_PROGRESS_` and an empty structure with data about the user (`user`)

TIP: In the response there may be other fields, e.g. `info`. These fields are described separately, and we shouldn't worry about them now icon:smile-o[]



== Identity check
The user identity is checked by sending the user to the address returned in the `url` field. So now open your browser and go to the page you got in this parameter. You should see the first screen of the identity checking process. For our sample strategy, it will be a screen where we can enter the data that the verification is to return.

After going through the process, you should be redirected to the `returnUrl` page that you entered when creating the conversation.


== Getting conversation result
Now let's check the conversation status. You should get request on url that was provided in `callbackUrl` field during creating conversation.


[source,json,indent=0]
.The callback request:
----
{
"id": "f109ad2b-5e3c-4f9d-b2ea-20379e56f101",
"created": "2020-12-24T16:00:00.930853456Z",
"target": "CONVERSATION",
"event": "FINISHED",
"payload": {
"conversation": {
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
"name":{
"firstName":"Jan",
"lastName":"Testowy"
}
}
}
}
}
}
}
}
----
This time the `status` has changed to `FINISHED`, which means the process is complete. At the same time, the `result` structure also contains the `FINISHED` state, which means that all the data was successfully determined. Retrieved data appeared in the `user` structure.

[.text-center]
*That's it. You managed to use API and get data.*
[.text-center]
*Congratulation!!*

== One more thing...
Authologic uses  `callbackUrl` to send you result of conversation. Regardless of that, if you need to check conversation status (for example during test, for debug purposes) you can ask about its condition at any time, using the method below.

Remember to adapt the conversation id in the address to your case:

[source, bash, indent = 0, role = "primary"]
.curl
----
curl -u my_login "https://sandbox.authologic.com/api/conversations/c12c1adc-3ff0-4d32-b95c-c593135c903e" \
-H "Accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json"
----

Assuming that you have finished the process, you should expect following response:

[source,json,indent=0]
.Response: Finished conversation status
----
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
"name":{
"firstName":"Jan",
"lastName":"Testowy"
}
}
}
}
}
}
----
TIP: In practice, checking the conversation status every now and then is not a good idea. Authologic is able to notify your system about the change of data related to the conversation using the `callback` mechanism. There is a separate document regarding callbacks xref:callback.adoc[document].

TIP: For purpose of better understanding, you may want to check status of the conversation in various stages of the process try to check status just after creation of the conversation, and after user has started identity check.

'''

include::include/pleaseHelp.adoc[]

xref:index.adoc[Back]
