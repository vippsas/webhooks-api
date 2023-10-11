---
title: Webhooks API Events
sidebar_label: Events
sidebar_position: 60
pagination_next: null
pagination_prev: null
---

# Events

Webhooks will send out events for the
[ePayment API](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks).
In the future, it may also send to other Vipps MobilePay APIs.

The event types to which you can subscribe are shown below.

## ePayment

| Name       | Event Type                      |
| ---------- | ------------------------------- |
| Created    | epayments.payment.created.v1    |
| Aborted    | epayments.payment.aborted.v1    |
| Expired    | epayments.payment.expired.v1    |
| Cancelled  | epayments.payment.cancelled.v1  |
| Captured   | epayments.payment.captured.v1   |
| Refunded   | epayments.payment.refunded.v1   |
| Authorized | epayments.payment.authorized.v1 |
| Terminated | epayments.payment.terminated.v1 |

See [ePayment Webhooks](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/features/webhooks) for the payload format.

## Recurring

| Name                   | Event Type                           |
| ---------------------- | ------------------------------------ |
| Agreement accepted     | recurring.agreement-activated.v1     |
| Agreement rejected     | recurring.agreement-rejected.v1      |
| Agreement stopped      | recurring.agreement-stopped.v1       |
| Agreement expired      | recurring.agreement-expired.v1       |
| Charge reserved        | recurring.charge-reserved.v1         |
| Charge refunded        | recurring.charge-refunded.v1         |
| Charge captured        | recurring.charge-captured.v1         |
| Charge cancelled       | recurring.charge-canceled.v1         |
| Charge failed          | recurring.charge-failed.v1           |
| Charge creation failed | recurring.charge-creation-failed.v1  |

## Qr

| Name       | Event Type                      |
| ---------- | ------------------------------- |
| CheckedIn  | user.checkin.v1                 |

See [QR Api](https://developer.vippsmobilepay.com/docs/APIs/qr-api/vipps-qr-api/#merchant-callback-qr-codes) for the payload format.
