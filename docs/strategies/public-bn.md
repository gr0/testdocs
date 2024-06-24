# Verification by Logging Into a Bank or a Penny Transfer

## Name
*public:bn*

## Supported products
- `identity`: identity verification
- `verify`: comparison with transferred data
- `bankTransactions`: retrieving of bank transactions (only when user selects logging in to the bank)

## Description
Identity verification, where the user is asked to select a bank, and then the verification method: open 
banking or making a transaction for the amount of PLN 0,01.

## Supported user fields
- PERSON_NAME_FIRSTNAME
- PERSON_NAME_LASTNAME
- PERSON_NAME_MIDDLE_INITIAL
- PERSON_NAME_MIDDLENAME
- PERSON_ADDRESS
- PERSON_IDS_ACCOUNTS
- COMPANY_NAME_NAME
- COMPANY_ADDRESS

### Email and Phone
Additionally, if the following fields were used in the query:
- PERSON_CONTACT_EMAIL_OTP
- PERSON_CONTACT_PHONE_OTP

The email or phone number is also confirmed using a one-time code.

## Parameters
n/a

## Notes action
n/a

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
