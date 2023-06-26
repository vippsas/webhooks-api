<!-- START_METADATA
---
title: Webhooks API Frequently Asked Questions
sidebar_label: FAQ
sidebar_position: 4
pagination_next: null
pagination_prev: null
---
END_METADATA -->

# Frequently asked questions

## How can I replace a webhook?

To replace a webhook, you can register a new webhook for the same event type.

After registration, the new webhook will receive the same traffic as the webhook
you want to replace.

You can now verify that the subscription works as expected before deleting the
old one.

Please do not let an obsolete webhook return an error (like `HTTP 404 Not Found`),
since that may be misclassified a real incident on our side, requiring us to
investigate the problem, contact you to find out what goes wrong, etc.

## Why do'nt I get any callbacks?

We require TLS 1.2 for the HTTPS connection to the webhooks you have registered.
If you do not support TLS 1.2, we will not be able to establish the connection,
and we are unable to send the callback.
