
<!-- START_METADATA
---
title: Quick start
sidebar_label: Quick start
sidebar_position: 2
pagination_next: null
pagination_prev: null
---
END_METADATA -->


For a quick start, you'll need to have set up the [Vipps API global Postman environment](https://developer.vippsmobilepay.com/docs/vipps-developers/getting-started/) and imported the [Webhooks Postman Collection](https://developer.vippsmobilepay.com/docs/APIs/webhooks-api/docs/). The following examples are for the ePayments API.

 ![Webhooks Postman Collection](/assets/postman-collection.png)

 ## Example of Use

 ### Register a webhook on the ePayments API capture event

 ```json
 POST /webhooks/v1/webhooks

 {
    "url": "<callbackUrl>",
    "events": ["epayments.payment.captured.v1"]
 }

 {

 }
 ```

### Get all current webhooks

```json
GET /webhooks/v1/webhooks

{

}

{
    "webhooks": [
        {
            "id": "dd99a450-7436-48af-8fc1-fbfb0453b2ec",
            "url": "<callbackUrl#1>",
            "events": [ "epayments.payment.captured.v1" ]
        },
        {
            "id": "04b99d37-3a67-4f36-8719-1593e08bf3d2",
            "url": "<callbackUrl#2>",
            "events": [ "epayments.payment.authorized.v1" ]
        }
    ]
}
```

### Delete webhook

```json
DELETE /webhooks/v1/webhooks/<webhook-id>

{

}
 ```

### Example of callback

```json
POST <callbackUrl#1>

x-ms-date: Thu, 30 Mar 2023 08:38:32 GMT  
x-ms-content-sha256: lNlsp1XA03N34HrQsVzPgJKtC+r7l/RBF4V3JQUWMj4=  
Authorization: HMAC-SHA256 SignedHeaders=x-ms-date;host;x-ms-content-sha256&Signature=agAiSyogQbDHpeucoNwYz+yAr5nJ+v+zasdkSbqzv+U=

{
    "msn": "98765",
    "reference": "4b2cde7acc0e4eaf86d32616d14e0cd1",
    "pspReference": "be62b9dafadc4448bc1e18ec2fee2fb3",
    "name": "CAPTURED",
    "amount": { "value": 100, "currency": "NOK" },
    "timestamp": "2023-07-29T10:23:23.9547273Z",
    "idempotencyKey": "425e20e63ea0402893179467c450bc2d",
    "success": true
}
```