# API: Transaction statistics

## Address
*GET /api/conversations/{conversationId}/bankTransactions/stats*

## Description
The method allows you to retrieve a series of statistics related to the transactions provided by the user.
The statistics always take into account transactions already performed, with the status `BOOKED` and `PENDING` 
(regardless of any additional flags provided when creating a conversation).

## Query example
n/a

## Query Parameter Description
The method supports the following query parameters:

| Parameter | Example | Description |
| --------- | ------- | ----------- |
| dateFrom | 2020-09-17T11: 18: 21.999Z | The starting date for the scope of analyzed transactions in the format https://tools.ietf.org/html/rfc3339[RFC3339^]. The default value is the oldest available transaction. You can enter an earlier date, but only transactions that the user has shared will be included. |
| dateTo | 2020-09-17T11: 18: 21.999Z | The end date for the range of analyzed transactions in the format https://tools.ietf.org/html/rfc3339[RFC3339^]. The default value is the latest available transaction. You can enter a later date, but only transactions that the user has shared will be included. |

## Sample response
<!--
title: "Example of the response with statistics"
-->
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

## Response Content Description

<!-- theme: info -->
> #### TIP
>
> Returned fields may be missing some information. For example, if only the account credits were 
> selected when creating a conversation, the statistics do not contain information about the charges.

Detailed description of returned fields:

| Parameter                               | Example                      | Description |
|-----------------------------------------|------------------------------| ----------- |
| dateFrom                                | 2020-09-16T10: 44: 51.544Z   | The starting date of the search criteria, or the date of the first transaction for all bank accounts, if the criteria was empty. The field will not be presented if the starting date criterion is not specified and there are no transactions in the given search criteria. |
| dateTo                                  | 2020-09-16T10: 44: 51.544Z   | End date of the search criteria, or the date of the last transaction for all bank accounts, if the criteria was empty. The field will not be presented if the end date criterion is not specified and there are no transactions in the given search criteria. |
| items                                   | -                            | A structure containing information about transaction statistics. Each element of this structure represents statistics from a separate bank account. |
| items.dateFirst                         | 2020-06-16T00: 00: 00.000Z   | Date of the first transaction in the range. |
| items.dateLast                          | 2020-09-16T00: 00: 00.000Z   | Date of the last transaction in the range. |
| items.numberOfCreditTransactions        | 12                           | Number of bank account discretionary transactions. |
| items.numberOfDebitTransactions         | 12                           | Number of debit transactions on the bank account. |
| items.avgCreditPerMonth                 | 300,000                      | Average value of credit transactions per month, presented in basic units - e.g. in grosze. The value will be available if the analyzed period is greater than 60 days. |
| items.avgDebitPerMonth                  | 258000                       | Average value of debit transactions per month, presented in basic units - e.g. in grosze. The value will be available if the analyzed period is greater than 60 days. |
| items.avgCredit                         | 30,000                       | Average value of bank account discretionary transactions, presented in basic units - e.g. in grosze. |
| items.avgDebit                          | 40,000                       | Average value of bank account debit transactions, presented in basic units - e.g. in grosze. |
| items.maxCredit                         | 110000                       | Maximum value of a bank account discretionary transaction, presented in basic units - e.g. in grosze. |
| items.maxDebit                          | 132000                       | The maximum value of the debit transaction from the bank account, presented in basic units - e.g. in grosze. |
| items.accountId                         | PL68249000050000400075212326 | Account number.                  |
| items.currency                          | PLN                          | Currency code for a given bank account. |

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com

