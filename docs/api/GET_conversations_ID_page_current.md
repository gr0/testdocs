# API: Get Information About the Current Page to be Displayed
 
## Address
*GET /api/conversations/{conversationId}/page/current*

## Description
Gets information about the current page that should be displayed to the user.

## Query Example
n/a

## Query Parameters Description
n/a

## Response example

<!--
title: "Format of the response for advanced UI"
-->
```json
{
    "render":{
      "page": "pageName",
      "redirect": "https://page.to.redirect/",
      "header": {
        "main": {
          "title": "Page title",
          "subtitle": "Page subtitle",
          "howItWorks": "Description of how the process works on a given page"
        },
        "group": {
          "title": "Subpage title",
          "subtitle": "Subpage subtitle",
          "howItWorks": "Description of how the process works on a given subpage"
        }
      },
      "args": {
        "list": ["value"],
        "obj": {
          "field": "value"
        }
      },
      "errors": {
        "fields": {
          "fieldName": "error description"
        },
        "accepted": {
          "fieldName": "correct value"
        },
        "rejected":{
          "fieldName": "denied value"
        },
        "globals": [
          "error description"
        ]
      },
      "reloadCurrent": false
    },
    "next": {
      "call": "nextPageID",
      "args": [
        "parameterName"
      ],
      "options": {
        "_optionName": ["value1", "value2"]
      },
      "async": 5
    }
}
```

## Description of the Response Content

Detailed description of the returned fields:

| Parameter | Required | Example | Description |
| --------- | -------- | ------- | ----------- |
| render.page | icon:times[] | baList | Name of the page that should be shown. If it is not present, it means that the user should be redirected to the page specified in `render.redirect`. |
| render.redirect | icon:check[] | https address | The address of the page to which the user should be redirected in order to continue the process. In this case, subsequent pages, if needed, will be generated by Authologic. If `render.page` is not present, redirection is mandatory. |
| render.header.main | icon:check[] | - | A section that defines page descriptions, i.e. the title, subtitle and description of how the process works on the page |
| render.header.main.title | icon:check[] | title | Page title |
| render.header.main.subtitle | icon:check[] | subtitle | Page subtitle |
| render.header.main.howItWorks | icon:check[] | action description | Description of how the process works on a given page |
| render.header.group | icon:check[] | - | Section defining subpage descriptions. A subpage can be defined, for example, when we have grouped data to present, where an additional sub-selection is possible for the selected element. An example of a section defining a subpage can be seen in the description of strategy [public:bn](../strategies/public-bn.md) |
| render.header.group.title | icon:check[] | title | Subpage title |
| render.header.group.subtitle | icon:check[] | subtitle | Subpage subtitle |
| render.header.group.howItWorks | icon:check[] | action description | Description of how the process works on a given subpage |
| render.args | icon:times[] | any json | Parameters necessary to display a given page, depending on a specific page. For example, for a page with a list of banks to choose from by the user, it will be a structure containing, among other things, information about available banks. |
| render.errors.fields | icon:times[] | map with field name and error description | A map specifying incorrectly entered form fields and a description of the associated error. |
| render.errors.accepted | icon:times[] | map containing the name of the field and its correctly given value | A map that specifies correctly entered form fields and the value of this field. For example, for a page with validation errors, but the values are also correct. |
| render.errors.rejected | icon:times[] | map containing the field name and its incorrect value | A map specifying incorrectly entered form fields and the value of this field. |
| render.errors.globals | icon:times[] | list of error descriptions | A list containing errors not related to specific form fields. |
| render.reloadCurrent | icon:times[] | true | Parameter informing that information about the next page should be obtained by calling the method `GET /api/conversations/{conversationId}/page/current`. It is used when the page is updated asynchronously (see `async` below). |
| next.call | icon:times[] | fd78cf43-12a7... | Name of the page to which the user information should be submitted. Information is sent via the method `POST /api/conversations/{conversationId}/page/{pageId}`. |
| next.args | icon:times[] | parameter name list | List of parameters that should be collected from the user and sent via the method `POST /api/conversations/{conversationId}/page/{pageId}`. |
| next.options | icon:times[] | parameter name list | Optional parameters that can be sent via the `POST /api/conversations/{conversationId}/page/{pageId}`  method instead of the required parameters defined in the `next.args` list. A detailed description and application of the optional parameters can be found in the description of the definition of specific pages. |
| next.async | icon:times[] | numerical value | The occurrence of this parameter informs that the current page should remain displayed for the user, and at the same time the method `POST /api/conversations/{conversationId}/page/{pageId}` should be called periodically with the page identifier contained in `next.call`. This option is used in all kinds of expectations for the end of the process. The numeric value of the `next.async` parameter specifies the minimum time in seconds between each invocation of the method. |

The field content may contain additional information about the format that needs to be modified before 
displaying, e.g. replacing with appropriate HTML tags.

There are currently two types of this information:
- links in the form of [Display Name] (URL).
- bold text in the form: \*text*

<!--
title: "Example of text with formatting"
-->
```json
{
  "disclaimer": "Link to the *Authologic* page is [here](https://www.authologic.com)"
}
```

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
