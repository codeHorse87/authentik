---
title: LearnWorlds
---

<span class="badge badge--secondary">Support level: Community</span>

## What is LearnWorlds

From https://www.learnworlds.com/

:::note
LearnWorlds is course platform for creating, selling and promoting online courses
:::

## Preparation

The following placeholders will be used:

-   `learnworlds.api` is the FQDN of the LearnWorlds authentication API endpoint. You can find the FQDN in Learnwords under `Site Builder > Sing in/up > SAML` when you copy the `Assertion Consumer Service (ACS) URL` as the FQDN of the URL.
-   `learnworlds.clientid` is the service account specific id of the url parameter *lw_client*. You can find the client id in Learnwords under `Site Builder > Sing in/up > SAML` when you copy the `Assertion Consumer Service (ACS) URL` as value of the parameter `lw_client`
-   `authentik.company` is the FQDN of the authentik install.
-   `authentik.application.slug` slug of the created application

Create an application in authentik. Create a SAML provider with the following parameters:

-   ACS URL: `https://learnworlds.api/saml/sp/saml2-acs?lw_client=learnworlds.clientid`
-   Issuer: `urn:authentik.company`
-   Servoce Provider Binding: Post
-   Audience: `https://learnworlds.api/saml/sp/metadata?lw_client=learnworlds.clientid`

Download the signing certificate of the provider you've created above.
Create an application, using the provider you've created above and note the slug of the application

## Budibase

In Learnwords under `Site Builder > Sing in/up > SAML` set the following values

-   IDP Identifier (Entity ID): `urn:authentik.company`
-   Sign-on URL: `https://authentik.company/application/saml/authentik.application.slug/sso/binding/init/)`
-   Identity Provider Certificate: Content of the authentik signing certificate you've downloaded above

Press `Save` at the top of the screen.
