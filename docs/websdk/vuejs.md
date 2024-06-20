# Integration Within the VueJS Application

If you are building your application using [VueJS](https://vuejs.org/), you must first add the Authologic library to your dependencies:

<!--
title: "Library Installation"
-->
```shell
npm i @authologic/websdk-vue
```

The next step is to import the library:

<!--
title: "Import in the page source"
-->
```javascript
import {AuthologicWidget} from '@authologic/websdk-vue'
```

and using the component in the page code:

<!--
title: "Component Usage"
-->
```html
<AuthologicWidget
    customerId="<customer ID>"
    conversationId="<conversation ID>"
    environment="sandbox"
/>
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
| `lang` | determined based on the browser | The two-letter interface language code, for example: `PL` |
| `theme` | determined by account configuration | Interface appearance. By default, it is configured on the Authlogic account side (see below) |
| `size` | {height: "650", width: "650"} | The screen size that the widget should occupy |

Appearance configuration example:

<!--
title: "Appearance Configuration Example"
-->
```javascript
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

Below is an example of a full page definition using the composition API:

<!--
title: "Page Example"
-->
```javascript
<template>
    <AuthologicWidget
            customerId="<customer ID>"
            conversationId="<conversation ID>"
            environment="sandbox"
            :theme="theme"
    />
</template>

<script setup lang="ts">
import {AuthologicWidget} from '@authologic/websdk-vue'

const theme = {
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

</script>
```

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
