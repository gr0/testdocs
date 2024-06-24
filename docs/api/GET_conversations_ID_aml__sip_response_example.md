#### SIP List Response Example

<!--
title: "Example of the response with AML verification data"
-->
```json
{
   "more":false,
   "items":[
      {
         "type":"PERSON",
         "score":0.87,
         "reason":"Special Interest Person (SIP) - Reputational Risk",
         "user":{
            "person":{
               "name":{
                  "firstName":"Vladimir",
                  "lastName":"Bautin",
                  "spellings":[
                     "Владимир Баутин"
                  ],
                  "alsoKnownAs":[
                     {
                        "firstName":"Владимир",
                        "lastName":"Баутин",
                        "title":"Original Script Name"
                     }
                  ]
               },
               "info":{
                  "nationality":"Russian",
                  "birthDate":"1948",
                  "deceased":false
               }
            }
         }
      }
   ]
}
```
