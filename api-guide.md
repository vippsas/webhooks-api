---
title: Webhooks API guide
sidebar_label: API guide
sidebar_position: 25
description: Find technical details about integrating with the Webhooks API.
pagination_prev: Null
pagination_next: Null
---

# API guide

Webhooks alert you to your API request updates (e.g., payment *Authorized*, *Cancelled*, *Expired*, and
[many others](https://developer.vippsmobilepay.com/docs/APIs/webhooks-api/events/)).

You can [register][register_webhook_endpoint]
to receive webhooks for specific events (e.g., *Cancelled* payment requests)
and update your system instantly upon notification.

**Note:**
You can register a set number of webhooks per event type for each sales unit.

For example, to register to receive a message for each authorized payment, send the following HTTP POST request:

[`POST:/webhooks/v1/webhooks`](https://developer.vippsmobilepay.com/api/webhooks/#tag/v1/paths/~1v1~1webhooks/post)

In the body of the request, specify the `"epayments.payment.authorized.v1"` in the `events` list.
Also, specify the `url` as the web server where we should send webhook messages. For example:

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

Use the `secret` to authenticate each webhook notifications with HMAC, as described in
[Request authentication](request-authentication.md).

Once a notification is authenticated, you will be able to get its payload.

Each API determines the format of their payloads.
The [payload from an ePayment webhook][epayment_events_url] is like this:

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

See [Events](events.md) for a list of all the events that you can subscribe to.


## Retries

Failed webhook notifications are retried with an exponential backoff for up to 7 days.
After all retries are exhausted, the notification is never sent again.
This applies to both new and previously created webhooks.

The delivery order of failed webhook notifications is guaranteed in order.
That means your server needs to accept the previous
failed request(s) for the same webhook before the next event notifications
can be sent.
Any response with HTTP status code in range 4-5xx will result in a retry.
Delay between retries will be progressively slower to not overwhelm receivers.




[register_webhook_endpoint]: https://developer.vippsmobilepay.com/api/webhooks/#tag/v1/paths/~1v1~1webhooks/post
[epayment_events_url]: https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks/
