# JavaScript Integration

In case you are not using any build mechanism, you can attach the script directly to the HTML page:

<!--
title: "Loading Script"
-->
```html
<script src="https://id.authologic.com/js/sdk.umd.cjs"></script>
```

Within the page, you need to define the place where the process should be displayed:

<!--
title: "Definition"
-->
```html
<div id="authologic"></div>
```

At the end of the page, before the end of the `<body>` tag, a script call should be placed in the `<script>` tag:

<!--
title: "Running the script"
-->
```javascript
init({
    customerId: '52569c18-1385-4ee2-b620-b49225946430',
    conversationId: '337f640c-66c2-484f-8068-b42b82d491f8',
    environment: 'sandbox'
})
```

<!-- theme: warning -->
> #### WARNING
>
> For testing you can use customerId: `development_only`. It will disable security, but will 
> only work in a sandbox environment.

Possible parameters are described below.

## Mandatory Parameters

| Name | Default value | Purpose |
| -------- | -------- | ------- |
| `customerId` | - | A dedicated SDK key, associated with the page where the widget is installed |
| `conversationId` | - | The ID of the conversation that should be started |

## Optional Parameters

| Name | Default value | Purpose |
| ------- | ------- | ------- |
| `environment` | production | The environment that will be used for the connection. Available values: production, sandbox |
| `divId` | authologic | The identifier of the HTML element in which the SDK will be embedded. Will be used if `element` is not defined. |
| `element` | - | HTML element in which the SDK will be embedded. |
| `lang` | determined based on the browser | The two-letter interface language code, for example: `PL` |
| `theme` | determined by account configuration | Interface appearance. By default, it is configured on the Authlogic account side (see below) |
| `size` | {height: "650", width: "650"} | The screen size that the widget should occupy |
| `onRedirect` | window.location.assign(url) | A function whose task is to open the continuation of the process in a new window, if required |

Appearance configuration example:

<!--
title: "Appearance Configuration Example"
-->
```html
theme: {
    primary: '#00ffb2',
    secondary: '#88ff00',
    background: '#a6715e',
    text: '#073d07',
    menu: {
        text: '#911111',
        background: '#a6715e'
    },
    item: {
        background: '#a6715e'
    },
    button: {
        text: '#021772'
    }
}
```

Below is an example of a full page:

<!--
title: "Page Example"
-->
```html
<!DOCTYPE html>
    <html lang="en">
    <head>
        <script src="https://id.authologic.com/js/sdk.umd.cjs"></script>
    </head>
    <body>
      <div id="authologic"></div>
      <script>
        AuthologicSDK.init({
            customerId: '<customerId>',
            divId: 'authologic',
            lang: 'pl',
            conversationId: '<conversationId>',
            environment: 'sandbox',
            size: {
                height: "700",
                width: "700"
            },
            theme: {
                primary: '#c2d9a9',
                background: '#2c282c',
                text: '#e5cfe5',
                menu: {
                    text: '#bebecc',
                    background: '#2a252a'
                },
                item: {
                    background: '#574d57'
                },
                button: {
                    text: '#e5cfe5'
                }
            }
          })
      </script>
    </body>
</html>
```

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
