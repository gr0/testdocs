# Detailed API Description

For people who prefer to have an encyclopedic overview of API capabilities in one place.

## Identity Verification Process

- [Create Conversation](api/POST_conversations.md)
- [Get Conversation State](api/GET_conversations_ID.md)
- [Callback Mechanism](api/callback.md)

## Bank Transactions

- [Downloading the Transaction List](api/GET_conversations_ID_bankTransactions.md)
- [Downloading the Account List](api/GET_conversations_ID_bankTransactions_accounts.md)
- [Downloading the Transaction Stats](api/GET_conversations_ID_bankTransactions_stats.md)

## AML

- [Downloading the AML Verification Data](api/GET_conversations_ID_aml.md)

## Additional Conversations’ data

- [Downloading Conversation Data Files](api/GET_conversations_ID_identity_metadata_media_ID.md)

## Advanced Methods

- [Turning off the Conversation](api/DELETE_conversations_ID.md)

## Advanced Personalization

- [Get Information about the Current page to be displayed](api/GET_conversations_ID_page_current.md)
- [Upload collected data and retrieve next page information](api/POST_conversations_ID_page_ID.md)
