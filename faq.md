---
title: FAQ
sidebar_position: 3
---

- [How to replace a webhook](#how-to-replace-a-webhook)


## How to replace a webhook

To replace a webhook, you should register a new webhook for the same events,
after registration the new webhook will recieve the same traffic as the webhook
you want to replace.

You can now verify that the new url works as expected before deleting the old
webhook.

Please do not let an obsolete webhook return 404s, since that may be
misclassified a real incident requiring us to reach out needlessly. 