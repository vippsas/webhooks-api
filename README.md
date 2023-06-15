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

You can subscribe to published *event types* by registering webhooks.
You will then be notified when any matching events are published for the
given sales unit ID.

As an example, a merchant can register a callback URL to receive a callback when
any of the merchant's payments are captured.

There is a set limit on how many registrations per event types per sales unit
are allowed. See the API reference for the exact limit.
