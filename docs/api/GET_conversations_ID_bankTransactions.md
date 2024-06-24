# API: Query for transaction list

## Address
*GET /api/conversations/{conversationId}/bankTransactions*

## Description

The method allows you to get user transactions, if the conversation contains them.
By default, it downloads transactions for a maximum of 90 full days, that is: today + 90 previous days. 
If you need a larger scope - please contact us. Transactions are returned as defined when creating the conversation. 
By default, this means both crediting and debiting the account, and only transactions that have already been 
made (posted or pending).

## Query Example
n/a

## Query Parameters Description
The method supports the following query parameters:

| Parameter | Example | Description |
| ------- | ------- | ------- |
| page | 10 | Page number. Paging starts on page 0 (default). |
| pageSize | 10 | Number of transactions on the results page. Currently, values above 200 are treated as 200. |

## Response Example

<!--
title: "Example of the response with transaction list"
-->
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
      "status": "BOOKED",
      "amount": 10030,
      "currency": "PLN",
      "title": "Account top up",
      "sender": "Jan Kowalski",
      "senderAccountId": "PL68249000050000400075212326",
      "recipient": "Jan Kowalski",
      "recipientAccountId": "PL32114020040000320250132522",
      "tags": ["internal"]
    }
  ]
}
```

## Response Content

Detailed description of returned fields:

| Parameter                             | Example | Description |
|---------------------------------------| ------- | ----------- |
| id                                    | 34df2bd6-b790-4560-9fc9-f86c86d87990  | Unique transaction identifier |
| date | 2020-08-27T10: 40: 28.348Z | Date of operation in UTC time |
| status | PENDING | Status of a given transaction at the time of downloading information from the bank. Allowed values: `BOOKED` - posted transaction, `PENDING` - transaction in progress, `SCHEDULED` - future transaction. Scheduled transactions appear when the `flags` field with the value` INCLUDE_SCHEDULED` was specified when creating the conversation. |
| bank | BREXPLPW | Bank where the transaction was performed. The value identifies the bank as the SWIFT / BIC code. |
| accountId | PL68249000050000400075212326 | Account number where transaction was registered. |
| type | DEBIT | Type of transaction. Available values: `DEBIT` (account debit) and `CREDIT` (account credit) |
| amount | 1000 | Value of the transaction in a currency unit, e.g. in grosze. |
| currency | PLN | type of currency |
| title | Account top-up | Transaction title |
| sender | Jan Kowalski | Transaction sender |
| senderAccountId | PL68249000050000400075212326 | Account number of the sender |
| recipient | Jan Kowalski | Recipient of the transaction |
| recipientAccountId | PL32114020040000320250132522 | Account number of the receiver |
| tags | ["monthly", "verification"] | Transaction categories |

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com


