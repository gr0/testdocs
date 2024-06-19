# Retrieving Information About User Transactions and Transaction Statistics

<!-- theme: info -->
> #### TIP
> 
> This document describes how to retrieve information about transactions. 
> [5 Minutes Integration](5minutesTutorial.md).

## Creating a conversation

In order to retrieve information about a transaction, you must create a conversation. Compared to the information contained 
in [5 Minutes Integration](5minutesTutorial.md) we need to define an additional product that we ask for: `bankTransactions`.
In the simplest case, nothing more needs to be added. Example:

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
        "bankTransactions": {
        }
    }
}'
```

Conversation defined this way, in response to a query about its status, returns an additional section:

```json
{
    "id":"c12c1adc-3ff0-4d32-b95c-c593135c903e",
    "userKey":"7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
    "url":"https://sandbox.authologic.com/c/c12c1adc-3ff0-4d32-b95c-c593135c903e",
    "status":"CREATED",
    "result":{
        "identity":{
            "status":"IN_PROGRESS",
            "user":{}
        },
        "bankTransactions": {
            "status":"IN_PROGRESS"
        }
    }
}
```

Info: `status` behaves identically to the `identity` section.

<!-- theme: info -->
> #### TIP
> 
> In practice, checking the conversation status every now and then is not a 
> good idea. Authologic is able to notify your system about the change of data related 
> to the conversation using the `callback` mechanism. There is a separate document regarding 
> callbacks [document](callback.md).

<!-- theme: warning -->
> #### WARNING
>
> In the target integration in practice the `callback` mechanism should always be used, because with a 
> greater number of checked conversations the query limit may be exceeded.

```json
{
    "id": "c12c1adc-3ff0-4d32-b95c-c593135c903e",
    "userKey":"7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
    "url":"https://sandbox.authologic.com/c/c12c1adc-3ff0-4d32-b95c-c593135c903e",
    "status": "FINISHED",
    "result": {
        "identity": {
            "status": "FINISHED",
            "user": {
                "person": {
                    "name": {
                        "firstName": "Maria",
                        "lastName": "Sochacka"
                    }
                }
            }
        },
        "bankTransactions": {
            "status": "FINISHED"
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

## Downloading Transactions

After finishing the conversation, we can retrieve the list of transactions using the query:

```shell
curl -u my_login "https://sandbox.authologic.com/api/conversations/c12c1adc-3ff0-4d32-b95c-c593135c903e/bankTransactions" \
-H "Accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json"
```

In the response we are getting the first page of results:

```json
{
    "more": true,
    "items": [
        {
            "id": "34df2bd6-b790-4560-9fc9-f86c86d87990",
            "date": "2020-08-27T10:40:28.348Z",
            "bank": "BREXPLPW",
            "accountId": "PL68249000050000400075212326",
            "type": "DEBIT",
            "amount": 10030,
            "currency": "PLN",
            "title": "Zasilenie konta",
            "sender": "Jan Kowalski",
            "senderAccountId": "PL68249000050000400075212326",
            "recipient": "Jan Kowalski",
            "recipientAccountId": "PL32114020040000320250132522",
            "tags": ["internal"]
        }
    ]
}
```

The key information here is the: `more`. If it has the value: `true`, then we can query for another page of results by adding the parameter: `page`:

```shell
curl -u my_login "https://sandbox.authologic.com/api/conversations/c12c1adc-3ff0-4d32-b95c-c593135c903e/bankTransactions?page=1" \
-H "accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json"
```

By modifying the parameter: `page`, we can retrieve subsequent pages of results until the response shows `more` set to `false`.

## Retrieving information about bank accounts

Another element is the possibility of additional information about the returned accounts for which the user has given us permissions.

```shell
curl -u my_login "https://sandbox.authologic.com/api/conversations/c12c1adc-3ff0-4d32-b95c-c593135c903e/bankTransactions/accounts" \
-H "accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json"
```

The response is a list of items for each account given to us, e.g .:

```json
{
    "items": [
        {
            "date": "2020-09-17T11:18:21.999Z",
            "balance": 10030,
            "bank": "BREXPLPW",
            "accountId": "PL68249000050000400075212326",
            "currency": "PLN",
            "activationDate": "2014-11-19"
        }
    ]
}
```

## Retrieving Transaction Statistics

Authologic also provides a number of transaction related statistics. Here you can see the simplest form, without e.g. 
specifying a date range. Details are traditionally described in 
[Transaction Statistics](api/GET_conversations_ID_bankTransactions_stats.md).

```shell
curl -u my_login "https://sandbox.authologic.com/api/conversations/c12c1adc-3ff0-4d32-b95c-c593135c903e/bankTransactions/stats" \
-H "accept: application/vnd.authologic.v1.1+json" \
-H "Content-Type: application/vnd.authologic.v1.1+json"
```

```json
{
    "dateFrom": "2020-09-16T10:44:51.544Z",
    "dateTo": "2020-09-16T10:44:51.544Z",
    "items": [
        {
            "dateFirst": "2020-06-16T00:00:00.000Z",
            "dateLast": "2020-09-16T00:00:00.000Z",
            "numberOfCreditTransactions": 12,
            "numberOfDebitTransactions": 12,
            "avgCreditPerMonth": 300000,
            "avgDebitPerMonth": 258000,
            "avgCredit": 30000,
            "avgDebit": 40000,
            "maxCredit": 110000,
            "maxDebit": 132000,
            "accountId": "PL68249000050000400075212326",
            "currency": "PLN"
        }
    ]
}
```

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
