# API: Account information

## Address
*GET /api/conversations/{conversationId}/bankTransactions/accounts*

## Description
The method allows you to retrieve information about bank accounts to which the user has delegated permissions.

## Example of a query
n/a

## Description of Query Parameters
n/a

## Sample Response

<!--
title: "Example of the response with a list of accounts"
-->
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

## Description of the Response Content

Detailed description of returned fields:

| Parameter | Example | Description |
| --------- | ------- | ----------- |
| date | 2020-09-17T11: 18: 21.999Z | Date on which the information was collected.|
| balance | 10030 | Account balance in a currency unit, e.g. in pennies. The value determines the balance of funds available on the account or, if there is no such information, the balance of funds booked. It may not occur if the bank does not provide the balance. |
| bank | BREXPLPW | Bank where the transaction was performed. The value identifies the bank as the SWIFT / BIC code. |
| accountId | PL68249000050000400075212326 | Account number. |
| currency | PLN | currency type | 
| activationDate | 2014-11-19 | The date when the account was opened or the date of the oldest transaction found. |

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
