---
title: Webhooks API Events
sidebar_label: Events
sidebar_position: 60
pagination_next: null
pagination_prev: null
---

# Events

Webhooks sends out events for the following APIs.

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
| Charge captured        | recurring.charge-captured.v1         |
| Charge cancelled       | recurring.charge-canceled.v1         |
| Charge failed          | recurring.charge-failed.v1           |

Recurring webhooks payload will be available soon

## QR

| Name       | Event Type                      |
| ---------- | ------------------------------- |
| CheckedIn  | user.checked-in.v1                 |

See [QR Webhooks](https://developer.vippsmobilepay.com/docs/APIs/qr-api/vipps-qr-api-webhooks/) for the payload format.
