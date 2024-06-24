# API: Metadata Information

## Address
*GET /api/conversations/{conversationId}/identity/metadata*

## Description
The method allows you to retrieve information about metadata collected as a result of the identity checking process.

### Query Example
n/a

## Query Parameters Description
n/a

## Response Example

<!--
title: "Example of the response with metadata list"
-->
```json
{
   "id":"9db8a804-4570-403e-9da6-162e608585e8",
   "list":{
      "media":[
         {
            "id":"7a4d1a9f-bdac-4d2c-96a6-bb51fb4ec7c5",
            "type":"DOCUMENT",
            "subtype":"ID_CARD",
            "variant":"BACK",
            "contentType":"image/png"
         },
         {
            "id":"679c492f-050a-4fb6-96fe-8b493640d762",
            "type":"FACE",
            "contentType":"image/png"
         },
         {
            "id":"7c16ab3d-3d20-43a1-a32e-7ea107d800b8",
            "type":"DOCUMENT",
            "subtype":"ID_CARD",
            "variant":"BACK",
            "contentType":"video/mp4"
         },
         {
            "id":"405ca76c-21a6-4bff-a944-e0de6550f1ea",
            "type":"FACE",
            "contentType":"video/mp4"
         },
         {
            "id":"89b8ff39-14ff-44d9-a646-501f7c5732d4",
            "type":"REPORT",
            "contentType":"application/pdf"
         }
      ]
   }
}
```

## Description of the response content
Detailed description of returned fields:

| Parameter | Example | Description |
| --------- | ------- | ----------- |
| id | 9db8a804-4570-403e-9da6-162e608585e8 | Conversation ID. |
| letter | - | A structure representing the set of metadata collected from the identity validation process. |
| list.media | - | List of information about available multimedia files. |
| list.media.id | 7a4d1a9f-bdac-4d2c-96a6-bb51fb4ec7c5 | The ID of the media file. |
| list.media.type | DOCUMENT | Media file type. Possible values: `DOCUMENT` - document of the authenticated person, `FACE` - face of the authenticated person, `REPORT` - report on the verification process |
| list.media.subtype | ID_CARD | The sub-type of the media file, such as the type of document. The value is blank if `type` = `FACE`. `ID_CARD` - identity card of the authenticated person, `DRIVER_LICENSE` - driving license of the authenticated person, `PASSPORT` - passport of the authenticated person, `RESIDENCE_PERMIT` - residence card of the authenticated person, `UTILITY_BILL` - proof of address of the authenticated person |
| list.media.variant | FRONT | Variant of the media file, e.g. document page. The value is blank if `type` = `FACE`. `FRONT` - front side of the document, `BACK` - back side of the document |
| list.media.contentType | image / png | The type of media file content. Example values: `image/png`, `video/mp4` |

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
