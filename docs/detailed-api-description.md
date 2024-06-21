## Detailed API Description
For people who prefer to have an encyclopedic overview of API capabilities in one place.

### Identity Verification Process

- [Create Conversation](api/POST_conversations.md)
- [Get Conversation State](api/GET_conversations_ID.md)
- [Callback Mechanism](api/callback.md)

### Bank Transactions

- [Downloading the transaction list](api/GET_conversations_ID_bankTransactions.md)
- [Downloading the account list](api/GET_conversations_ID_bankTransactions_accounts.md)
- [Downloading the transaction stats](api/GET_conversations_ID_bankTransactions_stats.md)

### AML

- [Downloading the AML verification data](api/GET_conversations_ID_aml.md)

### Additional Conversations’ data

- [Downloading conversation data files](api/GET_conversations_ID_identity_metadata_media_ID.md)

### Advanced Methods

- [Turning off the conversation](api/DELETE_conversations_ID.md)

### Advanced Personalization

- [Get information about the current page to be displayed](api/GET_conversations_ID_page_current.md)
- [Upload collected data and retrieve next page information](api/POST_conversations_ID_page_ID.md)
