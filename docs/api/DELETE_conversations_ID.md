# API: Turning Off Conversation

## Address
*DELETE /api/conversations/{conversationId}*

## Description
The method is used to change the conversation status to `EXPIRED` for an existing, not yet completed conversation. 
This may occur with a delay, and after successful turning off the conversation, a callback will be sent, if defined.

After that, any user starting the process will be immediately redirected to the `returnUrl` address provided when 
creating the conversation.

## Example of a Query
n/a

## Description of Query Parameters
n/a

## Example of a Reply
n/a

## Description of the Contents of the Reply
n/a

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
