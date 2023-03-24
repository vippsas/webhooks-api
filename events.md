<!-- START_METADATA
---
title: Webhooks API Events
sidebar_label: Events
sidebar_position: 2
pagination_next: null
pagination_prev: null
---
END_METADATA -->

💥 Work in progress 💥

The current list of event types that can be subscribed to.

## ePayments

| Name       | Event Type                      | Reference                                                                                                             |
| ---------- | ------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Created    | epayments.payment.created.v1    | [payload](https://vippsas.github.io/vipps-developer-docs/api/epayment#tag/QueryPayments/operation/getPaymentEventLog) |           
| Aborted    | epayments.payment.aborted.v1    | [payload](https://vippsas.github.io/vipps-developer-docs/api/epayment#tag/QueryPayments/operation/getPaymentEventLog) |           
| Expired    | epayments.payment.expired.v1    | [payload](https://vippsas.github.io/vipps-developer-docs/api/epayment#tag/QueryPayments/operation/getPaymentEventLog) |           
| Cancelled  | epayments.payment.cancelled.v1  | [payload](https://vippsas.github.io/vipps-developer-docs/api/epayment#tag/QueryPayments/operation/getPaymentEventLog) |           
| Captured   | epayments.payment.captured.v1   | [payload](https://vippsas.github.io/vipps-developer-docs/api/epayment#tag/QueryPayments/operation/getPaymentEventLog) |           
| Refunded   | epayments.payment.refunded.v1   | [payload](https://vippsas.github.io/vipps-developer-docs/api/epayment#tag/QueryPayments/operation/getPaymentEventLog) |           
| Authorized | epayments.payment.authorized.v1 | [payload](https://vippsas.github.io/vipps-developer-docs/api/epayment#tag/QueryPayments/operation/getPaymentEventLog) |           
| Terminated | epayments.payment.terminated.v1 | [payload](https://vippsas.github.io/vipps-developer-docs/api/epayment#tag/QueryPayments/operation/getPaymentEventLog) |           