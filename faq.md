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

💥 Work in progress 💥

## How to replace a webhook

To replace a webhook, you can register a new webhook for the same event type,
after registration, the new webhook will receive the same traffic as the webhook
you want to replace.

You can now verify that the subscription works as expected before deleting the
old one.

Please do not let an obsolete webhook return 404s, since that may be
misclassified a real incident requiring us to reach out needlessly.
