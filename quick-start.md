---
title: Quick start
sidebar_label: Quick start
id: quick-start
sidebar_position: 20
description: Quick steps for getting started with the Webhooks API.
toc_min_heading_level: 2
toc_max_heading_level: 5
pagination_next: null
pagination_prev: null
---

import ApiSchema from '@theme/ApiSchema';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Quick start

## Before you begin

The examples use standard example values that you must change to
use *your* values. This includes API keys, HTTP headers, reference, etc.

## Step 1 - Setup

You must have already signed up as an organization with Vipps MobilePay and have
your test credentials from the merchant portal.

You will need the following values, as described in the
[Getting started guide](https://developer.vippsmobilepay.com/docs/getting-started):

* `client_id` - Client_id for a test sales unit.
* `client_secret` - Client_id for a test sales unit.
* `Ocp-Apim-Subscription-Key` - Subscription key for a test sales unit.
* `merchantSerialNumber` - The unique ID for a test sales unit.
* `callbackUrl` - An HTTPS URL that can receive a POST request callback.

<Tabs 
    defaultValue="curl" 
    groupId="sdk-choice" 
    values={[ {label: 'curl', value: 'curl'}, {label: 'Postman', value: 'postman'}, ]}>

<TabItem value="postman">

**Please note:** To prevent your sensitive data and credentials from being synced to the Postman cloud,
store them in the *Current Value* fields of your Postman environment.

In Postman, import the following files:

Update the *Current Value* field in your Postman environment with your own credentials and callback URL.

* [Webhooks API Postman collection](/tools/Webhooks.postman_collection.json)
* [Global Postman environment](https://github.com/vippsas/vipps-developers/blob/master/tools/vipps-api-global-postman-environment.json).

🔥 **Don't store production keys in the cloud version of Postman, because this introduces a risk of exposure.** 🔥

Update the *Current Value* field in your Postman environment with your **Merchant Test** keys.
Use *Current Value* field for added security, as these values are not synced to the cloud.

</TabItem>

<TabItem value="curl">

No setup needed.

</TabItem>
</Tabs>

## Step 2 - Authentication

For the following steps, you will need an `access_token` from the
[Access token API](https://developer.vippsmobilepay.com/docs/APIs/access-token-api):
[`POST:/accesstoken/get`](https://developer.vippsmobilepay.com/api/access-token#tag/Authorization-Service/operation/fetchAuthorizationTokenUsingPost).
This provides you with access to the API.

<Tabs 
    defaultValue="curl" 
    groupId="sdk-choice" 
    values={[ {label: 'curl', value: 'curl'}, {label: 'Postman', value: 'postman'}, ]}> 
    
<TabItem value="postman">

```bash
Send request 'Get Access Token'
```

</TabItem>

<TabItem value="curl">

```bash
curl https://apitest.vipps.no/accessToken/get \
-H "client_id: YOUR-CLIENT-ID" \
-H "client_secret: YOUR-CLIENT-SECRET" \
-H "Ocp-Apim-Subscription-Key: YOUR-SUBSCRIPTION-KEY" \
-H "Merchant-Serial-Number: YOUR-MSN" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-H "Vipps-System-Plugin-Name: acme-webshop" \
-H "Vipps-System-Plugin-Version: 4.5.6" \
-X POST \
--data ''
```

</TabItem>
</Tabs>

The property `access_token` should be used for all other API requests in the `Authorization` header as the Bearer token.

## Step 3 - Register a webhook on the ePayment API capture event

<Tabs 
    defaultValue="curl" 
    groupId="sdk-choice" 
    values={[ {label: 'curl', value: 'curl'}, {label: 'Postman', value: 'postman'}, ]}> 
    
<TabItem value="postman">

```bash
Send request 'Register'
```

</TabItem>

<TabItem value="curl">

```bash
curl https://apitest.vipps.no/webhooks/v1/webhooks \
-H "Authorization: Bearer YOUR-ACCESS-TOKEN" \
-H "Ocp-Apim-Subscription-Key: YOUR-SUBSCRIPTION-KEY" \
-H "Merchant-Serial-Number: YOUR-MSN" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-H "Vipps-System-Plugin-Name: acme-webshop" \
-H "Vipps-System-Plugin-Version: 4.5.6" \
-X POST \
--data '{  
    "url": "<CALLBACK-URL>", 
    "events": ["epayments.payment.captured.v1"] 
}'
```

</TabItem>
</Tabs>

## Step 4 - Get all webhooks

<Tabs 
    defaultValue="curl" 
    groupId="sdk-choice" 
    values={[ {label: 'curl', value: 'curl'}, {label: 'Postman', value: 'postman'}, ]}> 
    
<TabItem value="postman">

```bash
Send request 'Get All'
```

</TabItem>

<TabItem value="curl">

```bash
curl https://apitest.vipps.no/webhooks/v1/webhooks \
-H "Authorization: Bearer YOUR-ACCESS-TOKEN" \
-H "Ocp-Apim-Subscription-Key: YOUR-SUBSCRIPTION-KEY" \
-H "Merchant-Serial-Number: YOUR-MSN" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-H "Vipps-System-Plugin-Name: acme-webshop" \
-H "Vipps-System-Plugin-Version: 4.5.6" \
-X GET \
--data ''
```

</TabItem>
</Tabs>

## Step 5 - Delete webhook

<Tabs 
    defaultValue="curl" 
    groupId="sdk-choice" 
    values={[ {label: 'curl', value: 'curl'}, {label: 'Postman', value: 'postman'}, ]}> 
    
<TabItem value="postman">

Variable `webhook_id` is automatically set when running request `Register`.

```bash
Send request 'Delete Last'
```

</TabItem>

<TabItem value="curl">

```bash
curl https://apitest.vipps.no/webhooks/v1/webhooks/<WEBHOOK-ID> \
-H "Authorization: Bearer YOUR-ACCESS-TOKEN" \
-H "Ocp-Apim-Subscription-Key: YOUR-SUBSCRIPTION-KEY" \
-H "Merchant-Serial-Number: YOUR-MSN" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-H "Vipps-System-Plugin-Name: acme-webshop" \
-H "Vipps-System-Plugin-Version: 4.5.6" \
-X DELETE \
--data ''
```

</TabItem>
</Tabs>
