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
* We send  updates and information to the webhook URL you have specified

You can **subscribe** to published **event types** by registering webhooks and
will then be **notified** when any matching events are published that match the
given sales unit's MSN (Merchant Serial Number).

As an example, a merchant can register a callback URL to receive a callback when
any of the merchant's payments are captured.

You can register for 5 webhooks per event type for each sales unit.
