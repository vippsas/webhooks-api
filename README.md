<!-- START_METADATA
---
title: Introduction to the Webhooks API
sidebar_label: Introduction
sidebar_position: 1
hide_table_of_contents: true
pagination_next: null
pagination_prev: null
---
END_METADATA -->

# Webhooks API

The API works this way:

* You register a webhook URL
* We send updates and information to the webhook URL you have specified

You can subscribe to published *event types* by registering webhooks.
You will then be notified when any matching events are published for the
given sales unit's Merchant Serial Number.

As an example, a merchant can register a callback URL to receive a callback when
any of the merchant's payments are captured.

You can register a set number of webhooks per event type for each sales unit.
See [Register webhook](https://developer.vippsmobilepay.com/api/webhooks/#tag/v1/paths/~1v1~1webhooks/post)
for details.