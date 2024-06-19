# User Verification Against AML lists

As part of the uniform API, Authologic allows you to check whether the user is on the AML lists. 
The response returns information on which lists the user's data has been found. Detailed information 
can also be downloaded.

In practice, there are two cases of checking:

## [AML verification combined with user identification](product-aml-with-identity.md) 
User verification is preceded by specifying information about the user and transferring the obtained information 
to check the presence on the AML lists.

## [AML verification based on the provided data](product-aml-without-identity.md) 
Determining whether the transferred data is on the AML lists. In this case, there is no need for user interaction.

## [AML change monitoring](product-aml-subscription.md)
You may also be interested in AML change monitoring.

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
