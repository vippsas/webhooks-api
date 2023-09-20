---
title: Webhooks API guide
sidebar_label: API guide
sidebar_position: 30
description: Find technical details about integrating with the Webhooks API.
pagination_prev: null
pagination_next: null
---

# API guide

![Vipps](./images/vipps.png) *All the features are available for Vipps now.*

![MobilePay](./images/mp.png) *Available for MobilePay in selected markets at the [Vipps MobilePay joint platform launch](https://www.vippsmobilepay.com/#about).*

You can use the Webhooks API to get an HTTP notification
whenever a subscribed event happens, for example a captured payment on the ePayment platform.

**Note:**
You can register a set number of webhooks per event type for each sales unit, as described in the
[API spec][register_webhook_endpoint].

As an example, to receive a message for each *Authorized* payment, send the following HTTP POST request:

[`POST:/webhooks/v1/webhooks`](https://developer.vippsmobilepay.com/api/webhooks/#tag/v1/paths/~1v1~1webhooks/post)

In the body, specify the `"epayments.payment.authorized.v1"`, as shown in the [Event table for ePayment](events.md#epayment).
Also, specify the `url` of the web server where we should send the webhook notifications. For example:

```json
{  
    "url": "https://example.com/mystore_website_backend",
    "events": ["epayments.payment.authorized.v1"]
}
```

You will receive a response similar to this:

```json
{
  "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
  "secret": "090a478d-37ff-4e77-970e-d457aeb26a3a"
}
```

Use the `secret` to authenticate the webhook notifications with HMAC, as described in
[Request authentication](request-authentication.md).
Once a notification is authenticated, you will be able to get its payload.
For example:

```json
{
    "msn": "123456",
    "reference": "24ab7cd6ef658155992",
    "pspReference": "1234567891",
    "name": "AUTHORIZED",
    "amount":
    {
        "currency": "NOK",
        "value": 35000
    },
    "timestamp": "2023-08-14T12:48:46.260Z",
    "idempotencyKey": "49ca711a9487112e1def",
    "success": true
}
```

Each API determines the format of their payloads.
The payload from an ePayment webhook is shown on the [ePayment API: Webhooks page][epayment_events_url].

See [Events](events.md) for a list of all subscribable events.

## Retries

Failed webhook notifications are retried with an exponential backoff for up to 7 days.
After all retries are exhausted, the notification is never sent again.
This applies to both new and previously created webhooks.

The delivery order of failed webhook notifications is guaranteed in order per registered webhook.
That means your server needs to accept all preceding requests for a given payment, before any new notifications can be received for the same payment.
For example, if you reply with an HTTP status code 500 to an authorization notification,
a new notification about the same payment being captured will not be sent
unless you reply with a successful HTTP status code to one of the retry attempts.

Any response with HTTP status code in range 4-5xx will result in a retry.
Delay between retries will be progressively slower to not overwhelm receivers.

[register_webhook_endpoint]: https://developer.vippsmobilepay.com/api/webhooks/#tag/v1/paths/~1v1~1webhooks/post
[epayment_events_url]: https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks/

## Partner Webhooks

As a partner, you can access endpoints with your usual key, client ID, and secret, without MSN.
Any webhooks registered by a partner will trigger for the subscribed events from ANY merchant registered the given partner.
