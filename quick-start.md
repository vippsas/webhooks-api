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

This document covers the quick steps for getting started with the Webhooks API.
You must have already signed up as an organization with Vipps MobilePay and have
your test credentials from the [Merchant Portal](https://portal.vipps.no), as described in the
[Getting started guide](https://developer.vippsmobilepay.com/docs/getting-started/).

For this quick start, you'll need the following.

* `client_id` - Merchant or Partner key required for getting the access token.
* `client_secret` - Merchant or Partner key required for getting the access token.
* `Ocp-Apim-Subscription-Key` - Merchant or Partner subscription key.
* `merchantSerialNumber` - Merchant ID if you're a Merchant.
* `callbackUrl` - Some HTTPS URL that can receive a POST request callback.

## Step 1 - Setup

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
-H "Merchant-Serial-Number: 123456" \
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
-H "Merchant-Serial-Number: 123456" \
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
-H "Merchant-Serial-Number: 123456" \
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
-H "Merchant-Serial-Number: 123456" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-H "Vipps-System-Plugin-Name: acme-webshop" \
-H "Vipps-System-Plugin-Version: 4.5.6" \
-X DELETE \
--data ''
```

</TabItem>
</Tabs>
