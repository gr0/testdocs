# Advanced Integration: Embed the Process Into Your Own Pages

<!-- theme: warning -->
> #### WARNING
> 
> THIS FEATURE IS EXPERIMENTAL! We want to be as open as possible and create Authologic together with you.
> That's why we sometimes share the first sketches of new features so that you can see them as soon as possible.
> Experimental functions may not work properly, and they may also change their API without prior notice. Therefore, 
> they are not yet suitable for production applications. However, if you are interested in this feature, this is a 
> good time to let us know about it and influence its final functionality so that it best suits your needs. Email 
> us at tech-support@authologic.com.

The basic version of integration involves redirecting the user to the address returned by the conversation creation API. 
This solution is simple, effective, and does not require additional integration work beyond defining the page to which 
the user will be redirected after the process is completed.

Authologic also provides the option to embed the verification process within your website. Unlike simple redirection, 
this solution requires you to take into account the following:

- this type of integration requires additional work,
- including the process within your website may require rebuilding the navigation,
- it should be taken into account that some verification methods require opening their own window,
- the webSDK code should be systematically updated

<!-- theme: warning -->
> #### WARNING
>
> Sites using WebSDK must be registered with Authologic. After providing Authologic with the website address, 
> you will receive the customer ID (`customerId`) necessary to run the integration. An invalid ID will result 
> in a browser CORS error.

<!-- theme: warning -->
> #### WARNING
>
> Conversation creation should also set the `layoutUrl` field pointing to the page where the webSDK is embedded. 
> Sometimes, there is a need to move process to another site and after the process is completed, Authologic must know 
> where to redirect the user.

Integration may look slightly different depending on the technologies you use:

## [Javascript](websdk/js.md) 
Integration directly into JavaScript when you don't use any framework.

## [React](websdk/react.md)
Integration within React applications.

## [Vue.js](websdk/vuejs.md)
Integration within the VueJS application.

## [Angular](websdk/angular.md)
Integration within the Angular application.

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
