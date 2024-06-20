# Additional Information About Verification Failure Reasons

In some cases, it may be important to know in detail why the verification was considered unsuccessful.
This is especially important when verifying with a photo of an ID document. The photo may be blurry, 
in which case it is worth repeating the verification. The reason for the refusal may also be an invalid 
document, in which case repeating the verification is pointless.

Authologic executes this scenario, returning a failure cause list as a result.
Example:

<!--
title: "Sample response containing the list of verification errors"
-->
```json
{
    "id": "2161d11b-24ff-1430-8635-e3d4dc138fff",
    "userKey": "ff97b4cc-81f4-413a-8bab-d0bd89da9a1f",
    "url": "https://id.sandbox.authologic.com/c/2161d11b-24ff-1430-8635-e3d4dc138fff",
    "status": "FINISHED",
    "result": {
        "identity": {
            "status": "FAILED",
            "errors": ["SCAN_DOCUMENT_NOT_DETECTED"],
            "user": {}
        }
    }
}
```

In the given example, we could not find the document in the photo.

Authologic returns the following grounds for refusal:

- `SCAN_GENERIC_ERROR`: Other errors associated with scanning documents
- `SCAN_DOCUMENT_NOT_DETECTED`: Document not detected in the picture
- `SCAN_DOCUMENT_TYPE_MISMATCH`: given a different type than the actual scanned document
- `SCAN_DOCUMENT_EXPIRED`: The expiration date of the document passed
- `SCAN_DOCUMENT_SIDE_MISMATCH`: Document page not shown
- `SCAN_DOCUMENT_NOT_SUPPORTED`: This document type is not supported by the vendor
- `SCAN_DOCUMENT_TOO_BLURRY`: Document photo too blurry
- `SCAN_FACE_UNCERTAIN`: Unable to confirm
- `SCAN_FACE_MISMATCH`: The face does not match the face in the photo
- `FRAUD_SUSPICION`: Suspected fraud
- `SCAN_DOCUMENT_COUNTRY_MISMATCH`: The country selected by the user does not match the document
- `SCAN_DOCUMENT_DAMAGED`: The document is corrupted in some way
- `SCAN_DOCUMENT_NOT_FULLY_VISIBLE`: Document not fully visible
- `SCAN_DOCUMENT_READ_FAILED_ID`: Could not read document number
- `SCAN_DOCUMENT_READ_FAILED_NATIONAL_ID`: Failed to read user ID
- `SCAN_DOCUMENT_READ_FAILED_FIRSTNAME`: Failed to read name
- `SCAN_DOCUMENT_READ_FAILED_LASTNAME`: Could not read name
- `SCAN_DOCUMENT_READ_FAILED_ISSUE_DATE`: Failed to read document issue date
- `SCAN_DOCUMENT_READ_FAILED_EXPIRY_DATE`: Failed to read document expiration date
- `SCAN_DOCUMENT_READ_FAILED_BIRTHDATE`: Date of birth could not be read
- `SCAN_DOCUMENT_MRZ_NOT_DETECTED`: The document MRZ data could not be found
- `SCAN_DOCUMENT_MRZ_READ_FAILED`: Could not read document MRZ data
- `SCAN_DOCUMENT_PROBABLY_FAKE`: The document may be bogus
- `SCAN_FACE_TOO_MANY_PEOPLE`: More people have been detected in the photo
- `SCAN_FACE_TOO_BLURRY`: Photo of the fase is too blurry
- `SCAN_FACE_NOT_DETECTED`: No face detected on the photo
- `ABANDONED`: User abandoned the verification process
- `ELECTRONIC_DOCUMENT_ACCESS_ERROR` - Failed to read the electronic layer of the document or wrong PIN number provided
- `BANK_NO_ACCOUNTS_SHARED` - The user has not selected an account on the bank's side or the accounts have not been made available
- `NO_DATA_SHARED` - User authentication or authorization process has not been completed based on a user action e.g. user rejected to share personal data, user cancelled process on identity provider side
- `INSUFFICIENT_AGE` - User has insufficient age to perform operation requested by identity service provider
- `NO_IDENTITY_FOUND` - The end user does not have an identity that matches the assumptions made by the identity provider e.g. user not eligible
- `INSUFFICIENT_PRIVILEGES` - The user has insufficient privileges to perform operation requested by identity service provider e.g. user has an account with limited access
- `NO_USER_FOUND` - The user account was not found by identity service provider e.g. the identity provider could not find the user account associated with the specified national identification number
- `PROVIDER_SERVER_ERROR` - Provider has returned technical error (for example internal server error)
- `PROVIDER_UNAVAILABLE` - There is a problem with connecting to provider's system(s)
- `USER_NOT_AUTHORIZED` - The user could not be authorized due to providing wrong password, pin, code tec.

<!-- theme: warning -->
> #### WARNING
>
> The reason list depends on the verification method. We are also constantly working on identifying further 
> reasons for refusal, so you should not assume in your code that this list is final.

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
