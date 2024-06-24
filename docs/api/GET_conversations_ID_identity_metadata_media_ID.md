# API: Media File Download

## Address
*GET /api/conversations/{conversationId}/identity/metadata/media/{id}*

## Description
The method allows you to download a media file based on its identifier. The file ID 
should be obtained from a method that returns metadata information.

## Query Example
n/a

## Query Parameter Description
n/a

## Response Example
n/a

## Response Content Description 
If the answer is successful, the data stream will be provided along with the following key HTTP headers:

| Header | Example | Description |
| ------ | ------- | ----------- |
| content-disposition | attachment; filename = 9db8a804-4570-403e-9da6-162e608585e8_idi_ID_CARD_BACK.png | The file name is generated based on information about the media file. |
| content-type | image / png | The type of multimedia file content, similar to the one presented in the information about the given file. |
| status | 200 | Response status. |


In case of a wrong answer, the error information will be passed in the format `application/vnd.authologic.v1.1+json`.

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
