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

💥 Work in progress 💥

You can **subscribe** to published **event types** by registering webhooks and
will then be **notified** when any matching events are published that match the
given sales unit id.

As an example, a merchant can register a callback url to receive a callback when
any of the payments of the merchant is captured.

There is a set limit on how many registrations per event types per sales unit
allowed, see the API reference for the exact limit.

## Index

- [Introduction](webhooks-api)
- [Event Types](webhooks-api/events)
- [Frequent Asked Questions](webhooks-api/faq)
- [API Reference](/api/webhooks)