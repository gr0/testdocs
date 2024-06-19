# Strategy Testing Information

Authologic provides many integrations of different types and features. How these integrations are tested 
depends on the capabilities provided by each vendor.

Usually during development, the best practice is to use [public:sandbox](strategies/public-sandbox.md). It allows you to conveniently determine the results of a given verification, which facilitates integration and testing of individual cases.

However, sometimes it is necessary to see what the full process will look like. If the provider includes such a possibility, it is also made available by Authologic.

However, some suppliers do not allow testing or such testing is difficult or limited. Below is a list of such cases:

| Vendor | Description |
| ------- | ------- |
| eDO App | Verification requires a test application and a test document in the form of a plastic card. |
| Idenfy | The returned data do not include manual verification and correction of results. |
| Contacts | Verification of the phone number and email address in the test version does not send SMS/email and the code is fixed. |
| MojeID | The provider only provides a low-level simulator requiring knowledge of the communication protocol. In practice, this provides a subset of the capabilities of the `public:sandbox` strategy. |

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
