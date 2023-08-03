<!-- START_METADATA
---
title: Webhooks API Events
sidebar_label: Events
sidebar_position: 3
pagination_next: null
pagination_prev: null
---
END_METADATA -->

# Events

Webhooks will send out events for the
[ePayment API](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks),
but in the future, it may also send to other Vipps MobilePay payment APIs.

The event types to which you can subscribe are shown below.

## ePayment

| Name       | Event Type                      | Reference|
| ---------- | ------------------------------- | ---------|
| Created    | epayments.payment.created.v1    | [payload](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks) |
| Aborted    | epayments.payment.aborted.v1    | [payload](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks) |
| Expired    | epayments.payment.expired.v1    | [payload](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks) |
| Cancelled  | epayments.payment.cancelled.v1  | [payload](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks) |
| Captured   | epayments.payment.captured.v1   | [payload](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks) |
| Refunded   | epayments.payment.refunded.v1   | [payload](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks) |
| Authorized | epayments.payment.authorized.v1 | [payload](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks) |
| Terminated | epayments.payment.terminated.v1 | [payload](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks) |

See the [payload specification](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks) for more information.
