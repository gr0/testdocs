# Documentation

<!-- theme: info -->
> Authologic allows you to execute a simple and effective verification of the user's identity. 
> The use of the API consists of initiating the process by an external system, redirecting the 
> user to the appropriate page, and then receiving the verification results.

## Organization of the Documentation
Documentation is structured to take you from the simpler to the more advanced options.
Our API is also built in such a way that you don’t have to make all the decisions related to integration right away. 
Each element is only a supplement to the previous ones. This allows you to quickly build a basic integration, then add 
new features, products, and enhancements when needed.

## Basic Information
The following information is *necessary* to build a basic, but in most cases sufficient, Authologic integration.

#### [Overview](overview.md) 
Understand communicating with Authologic services and how to verify identity.

#### [Integration in 5 minutes:Basic information](5minutesTutorial.md)
API in practice, which is a description of the basics of integration on the basis of a few commands that can be 
tested from the command line.

#### [Conversation statuses](statuses.md)
Description of the conversation lifecycle, conversation status and individual products.

#### [Using change notifications with callbacks](callback.md)
How Authologic notifies you of the result of a verification.

#### [Implementation Notes](implementation.md)
What you should pay attention to while developing and how we will make changes to the API in the future.

#### [Strategy Testing](testing.md)
Information on testing the strategy

#### [Production Launch](golive.md)
How to make the integration available to your users.

## What's Next?
The _basic information_ should be sufficient to do basic integration. However, depending on your needs, 
integration can be expanded in various directions. Below you will find chapters that should cover specific topics.

### Strategies

#### [Verification Strategies](strategies.md) 
In case you want to use several verification methods, e.g. depending on how sensitive the operation your user wants to perform.

### Products
In addition to the basic and always available information about the verified user, Authologic provides additional elements 
called products. They are described below.

#### [Transactions](product-bankTransactions.md)
Retrieving information about a user's transactions and statistics related to those transactions.

#### [Data Verification](product-verify.md)
Compare the verification data with the submitted data.

#### [User authentication](product-auth.md) 
A product that allows you to build mechanisms for logging into your system.

#### [AML Verification](product-aml.md) 
User verification for presence on AML lists.

You may also be interested in [AML change monitoring](product-aml-subscription.md).

### Additional Options and Extensions

#### [Embedding the Process Within your Website](websdk.md)
How to embed the verification process on your own website.

#### [Downloading Captured Photos and Other Verification Data](addon-metadata.md)
How to access original scans of a document and user's photos.

#### [Additional Information about the Verification Process](addon-info.md)
How to check which method was selected by the user.

#### [Additional Information about Verification Failure Reasons](addon-errors.md)
How to check the reason for refusal to verify and detailed information about its progress.

#### [Additional Validations of the Verification Process](addon-checks.md)
How to check the additional validations performed on the user data.

#### [Possibility to Disable Unfinished Conversations](addon-expire.md)
How to block the ability to pass ID verification for a specific conversation.

### FAQ: Frequently Asked Questions

#### [Foreign Translation and Support](i18n.md)
How to handle the multilingual interface.

#### [Use of Mandatory and Optional Fields](addon-mandatoryAndOptionalQueries.md)
When to use `query.requireOneOf` and `query.optional`.

#### [Using Hints](addon-hints.md)
Define `hints` fields.

#### [Changing Appearance](customLayout.md)
Options available for customizing the user interface.

### Development

#### [Versions and Unsupported Features](deprecations.md)
Information about functionalities that will be removed and may require updating your system.

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


<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
