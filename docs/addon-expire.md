# Possibility to Disable Unfinished Conversations

Once created, the conversation allows the user to go through the verification process. This is possible until:

- the verification is completed
- the user will terminate the process
- the time related to the retention settings has passed, after which the conversation is ended with the status `EXPIRED`

In some cases, it is necessary to end the conversation early. For this purpose, Authologic provides an appropriate API method 
described [here](api/DELETE_conversations_ID.md).

After calling this method, the conversation enters the `EXPIRED` state. The user can still enter the process address, but 
will be automatically redirected to the `returnUrl` address defined when creating the conversation.

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com

