# Implementation Notes

## Security and API Logging

The API supports HTTP Basic authentication. This method requires a username and password.

<!-- theme: warning -->
> #### WARNING
>
> The username is the same as your account name, while the password is *API dedicated* and 
> dependent on the environment you are using.

Communication always takes place using the HTTPS protocol. In the case of the `callback` mechanism, 
inquiries are signed, which allows for the verification of the sender. In a production environment, 
the `callback` address on your side must use HTTPS. In the case of a test environment, this is not 
necessary.

## API versioning and making changes

The current API version should be highlighted in the query in the `Content-Type` and `Accept` headers.
The current content of these fields for API version 1.1 is: `application/vnd.authologic.v1.1+json`

The API changes from time to time. In the case of minor changes that do not affect the existing implementations, 
they are applied without changing the API version number. To prevent them from conflicting with existing integrations, 
those rules were adopted:

<!-- theme: warning -->
> #### WARNING
>
> Pay attention to the rules below. It is very important to follow them so that changes to the API do not 
> affect your integration.

- Any new fields appearing in the API response should be ignored. 
- Additional API methods may appear at any time.
- New arguments may appear in parameters, but they will always be optional.
- There may be new error explanations, although the response statuses remain the same and still indicate the nature of the error.
- The order of fields in the answer may change.
- The way the answer is formatted may change.

## Date formats

Datetime formats are in the [RFC3339](https://tools.ietf.org/html/rfc3339) format. Authologic always returns full dates in 
UTC, e.g. `2020-09-17T11:18:21.999Z`. API accepts data in UTC or time zone format. Examples of valid dates:

- `2020-04-02T09:00Z`
- `2020-04-02T09:20:50Z`
- `2020-04-02T09:20:50.322Z`
- `2020-09-01T13:15-05:00`
- `2020-09-01T13:15:22+02:00`

The dates themselves (e.g. dates of birth) are given in the format without the hour part, e.g.:

- `2020-04-02`
- `2020-07-30`

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
