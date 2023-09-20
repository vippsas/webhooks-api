---
title: Introduction to the Webhooks API
sidebar_label: Introduction
sidebar_position: 1
hide_table_of_contents: true
pagination_next: null
pagination_prev: null
---

# Webhooks API

![Vipps](./images/vipps.png) *All the features are available for Vipps now.*

![MobilePay](./images/mp.png) *Available for MobilePay in selected markets at the [Vipps MobilePay joint platform launch](https://www.vippsmobilepay.com/#about).*

The API works this way:

* You register a webhook URL
* We send updates and information to the webhook URL you have specified

You can subscribe to published *event types* by registering webhooks.
You will then be notified when any matching events are published for the
given sales unit's Merchant Serial Number.

The Webhooks API supports:

* [ePayment API](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/)
* [QR API: Merchant Callback QR codes](https://developer.vippsmobilepay.com/docs/APIs/qr-api/vipps-qr-api/#merchant-callback-qr-codes) (*coming soon*)

## Next steps

* [API quick start](quick-start.md): Run the basic examples in curl or Postman.
* [API guide](api-guide.md): Learn about the Webhooks API.
* [Events](events.md): See the events you can register for.
* [Request Authentication](request-authentication.md) - Learn how to authenticate the webhooks.
* [API FAQ](faq.md): Look for your question among those people have asked before.
* [API spec](https://developer.vippsmobilepay.com/api/webhooks/): Go to the endpoint specifications.

If you're new to the platform, see
[Getting started](https://developer.vippsmobilepay.com/docs/getting-started/)
for information about API keys, product activation, and the test environment.
