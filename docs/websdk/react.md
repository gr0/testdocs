# Integration Within React Applications

If you are building your application using [React](https://react.dev/), you must first add the Authologic library to your dependencies:

<!--
title: "Library installation"
-->
```shell
npm i @authologic/websdk-react
```

The next step is to import the library:

<!--
title: "Import in page definition"
-->
```javascript
import {AuthologicWidget, Theme} from "@authologic/websdk-react";
```

and using the component in the page:

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
title: "Appearance configuration example"
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
import {AuthologicWidget, Theme} from "@authologic/websdk-react";

const theme: Theme = {
    button: {
        text: "#e5cfe5"
    },
    menu: {
        background: "#537743",
        text: "#e5cfe5"
    },
    primary: "#537743",
    background: "#242424",
    secondary: "#c9afd2",
    text: "#537743",
    item: {
        background: "#e5cfe5"
    }
}

function App() {
    return (
        <>
          <div>
              <AuthologicWidget
                  customerId="development_only"
                  conversationId="3fccdba0-8ff7-407b-93a0-1f2f7ea4855b"
                  environment="sandbox"
                  theme={theme}
              />
          </div>
        </>
    )
}

export default App
```

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
