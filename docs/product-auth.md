# User Authentication

Authologic allows you to build a user login process (access authentication) to your system. To do this, the 
user must first register. After user registration, the user can be authenticated at any time.

<!-- theme: info -->
> #### TIP
> 
> The document complements [Integration in 5 minutes](5minutesTutorial.md).

## Registration

Registration involves adding the `auth` section when creating a conversation:

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
        "auth": {
        }
    }
}'
```

The conversation constructed this way will also return user data. If this is not required, simply omit the `identity` section:

```shell
curl -X POST -u my_login "https://sandbox.authologic.com/api/conversations" \
-H "accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json" \
-d '{
    "userKey": "7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
    "returnUrl": "https://authologic.com/tests/return/?conversation={conversationId}",
    "query": {
        "auth": {
        }
    }
}'
```

After the user has gone through such a process and the conversation has been completed correctly, additional 
data will appear in the response in the `auth` section, allowing for future user authentication. The exact 
content depends on the specifics of the authentication method.

<!-- theme: warning -->
> #### WARNING
>
> Not all strategies support authentication. If you use a strategy that does not support this product, the 
> strategy will not return authentication data.

## User Identification Methods

Some verification methods are able to determine the user themselves. In this case, simply redirect the user to 
the authentication process. For such methods, a `token` is returned during registration - a unique user identifier. 
The response always contains the following section:

```json
"auth": {
  "status": "FINISHED",
  "token": "d42115b0-58d3-4e9b-b970-12ca7de181c7"
}
```

A `Token` is a unique key associated with a user and authentication method. Each time this user authenticates using 
this method, this token will be returned.

<!-- theme: info -->
> #### TIP
>
> A user can have multiple tokens if you allow them to use different authentication methods.

## Methods Verifying Specified User

Some verification methods are only able to answer the question whether the user is who he or she 
claims to be. This method requires providing additional information that indicates the user who will 
be authenticated. For such methods, `token` - a unique user identifier and `challenge` - the equivalent 
of a login, are returned during registration. The response then contains the following section:

```json
"auth": {
  "status": "FINISHED",
  "token": "d42115b0-58d3-4e9b-b970-12ca7de181c7",
  "challenge": "2e3c01a8-a983-4024-acc9-8005c57d10af"
}
```

A `Token` is a unique key associated with a user and authentication method. `Challenge` specifies 
the user to be verified. Each time this user authenticates using this method, the appropriate `challenge` 
must be sent - after successful authentication, the above token will be returned.

<!-- theme: info -->
> #### TIP
>
> A user can have multiple challenge / token pairs if you allow them to use different authentication methods.

## Authentication

Once the user has successfully registered, authentication operations can be performed. This means creating a 
conversation with an `auth` section. There are some minor differences depending on the method used, described below.

## User Identification Methods

For such methods, a sample conversation might look like this:

```shell
curl -X POST -u my_login "https://sandbox.authologic.com/api/conversations" \
-H "accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json" \
-d '{
  "userKey": "7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
  "returnUrl": "https://authologic.com/tests/return/?conversation={conversationId}",
  "query": {
    "auth": {
    }
  }
}'
```

As you can see, authentication in practice is no different from registration. After going through the process, the response may contain the following section:

```json
"auth": {
  "status": "FINISHED",
  "token": "d42115b0-58d3-4e9b-b970-12ca7de181c7"
}
```

`Token` directly identifies which user has passed authentication.

## Methods that verify the specified user

For such methods, a sample conversation might look like this:

```shell
curl -X POST -u my_login "https://sandbox.authologic.com/api/conversations" \
-H "accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json" \
-d '{
  "userKey": "7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
  "returnUrl": "https://authologic.com/tests/return/?conversation={conversationId}",
  "query": {
    "auth": {
      "challenge": "2e3c01a8-a983-4024-acc9-8005c57d10af"
    }
  }
}'
```

In this model, it is necessary to provide `challenge` for the method to be able to determine 
which user it is verifying. After going through the process, the response may contain the 
following section:

```json
"auth": {
  "status": "FINISHED",
  "token": "d42115b0-58d3-4e9b-b970-12ca7de181c7",
  "challenge": "2e3c01a8-a983-4024-acc9-8005c57d10af"
}
```

`Token` directly identifies which user has passed authentication. `Challenge` should match the value 
provided when creating the conversation.

<!-- theme: warning -->
> #### WARNING
> 
> If an unknown `challenge` value was provided when creating a conversation, the conversation will be 
> automatically closed with the status `FINISHED`. The status of the `auth` product in this case will 
> be `FAILED`.

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
