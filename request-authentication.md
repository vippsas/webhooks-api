---
title: Webhooks API Request authentication
sidebar_label: Request authentication
sidebar_position: 50
pagination_next: null
pagination_prev: null
---

import ApiSchema from '@theme/ApiSchema';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Request authentication

A notification request from webhooks can be verified by using the `host`, `x-ms-date`, `x-ms-content-sha256`, and `authorization` headers with the
unique secret received when the webhook was registered. The authorization is a
sha256 HMAC hash of the request date, content, and URI that is created using the
webhook secret.

<Tabs
    defaultValue="js" 
    groupId="example-choice" 
    values={[ {label: 'JavaScript', value: 'js'}, {label: '.Net C#', value: 'csharp'}, ]}>

<TabItem value="js">

To run: `node webhook.mjs`
```js
import crypto from "crypto";

// The secret is found in the response body when you register a webhook. 
// Note: The secret is unique per hook registration (EventType+YourURL).
const secret = 'A0+AeKBRG2KRGvnNwJpQlb6IJFk48CKXCIcrLoHncVJKDILsQSxS6NWCccwWm6r6FhGKhiHTBsG2wo/xU6FY/A=='

// The complete url of the webhook, including query parameters if applicable. I.e. https://yoursite.com/webhooks/vmp/v1
const requestUrl = "https://webhook.site/e2cee29b-012e-4f1d-8ef4-e95fd74a7a63"
// Part of the HTTP request header from Vipps MobilePay, found in the field 'x-ms-date'
const dateTime = "Thu, 30 Mar 2023 08:38:32 GMT"

// The signature/authorization sent by Vipps MobilePay for you to verify against. 
// Part of the HTTP request header from Vipps MobilePay, found in the field 'authorization'
const actualSignature = "HMAC-SHA256 SignedHeaders=x-ms-date;host;x-ms-content-sha256&Signature=agAiSyogQbDHpeucoNwYz+yAr5nJ+v+zasdkSbqzv+U="

// HTTP Body
const payloadJson = {
  "some-unique-content":"ee6e441b-cc4a-46f8-895d-a5af79bcc233/hello-world"
}

const hashedPayload =  crypto.createHash("sha256").update(JSON.stringify(payloadJson)).digest("base64")
// returns 'lNlsp1XA03N34HrQsVzPgJKtC+r7l/RBF4V3JQUWMj4='

// The complete url of the call to the webhook, including query parameters if applicable
const url = new URL(requestUrl)
const pathAndQuery = url.pathname + url.search; 
// returns '/e2cee29b-012e-4f1d-8ef4-e95fd74a7a63'
const host = url.host 
// returns 'webhook.site'

// Example is using HTTP POST, hence starting with 'POST\n'
const expectedSignedString = `POST\n${pathAndQuery}\n${dateTime};${host};${hashedPayload}`
/* returns:
POST
/e2cee29b-012e-4f1d-8ef4-e95fd74a7a63
Thu, 30 Mar 2023 08:38:32 GMT;webhook.site;lNlsp1XA03N34HrQsVzPgJKtC+r7l/RBF4V3JQUWMj4=
*/

// Run the HMAC algorithm on the expectedSignedString with the secret for the hook
const expectedSignature = crypto.createHmac("sha256", secret)
  .update(expectedSignedString)
  .digest("base64")
// returns 'agAiSyogQbDHpeucoNwYz+yAr5nJ+v+zasdkSbqzv+U=' 
// which matches the expected signature

const expectedAuth = `HMAC-SHA256 SignedHeaders=x-ms-date;host;x-ms-content-sha256&Signature=${expectedSignature}`

if(expectedAuth !== actualSignature) {
  // Log the error.
  // Fail, stop processing
  throw new Error('Authorization fields do not match expected value!');
}
// Continue with business logic related to the webhook.
console.log('Success! Business logic awaits!')
```
</TabItem>

<TabItem value="csharp">

## Summary pseudocode

```cmd
let contentHash = hash(serializedContent)

let signatureText = POST\n{pathAndQuery}\n{date};{authority};{contentHash}
let signature = sign(secret, signatureText)
let authorization = HMAC-SHA256 SignedHeaders=x-ms-date;host;x-ms-content-sha256&Signature={signature}
```

## Sample values

```cmd
Given values
  let secret = A0+AeKBRG2KRGvnNwJpQlb6IJFk48CKXCIcrLoHncVJKDILsQSxS6NWCccwWm6r6FhGKhiHTBsG2wo/xU6FY/A==
  let url = https://webhook.site/e2cee29b-012e-4f1d-8ef4-e95fd74a7a63
  let content = {"some-unique-content":"ee6e441b-cc4a-46f8-895d-a5af79bcc233/hello-world"}
  let date = Thu, 30 Mar 2023 08:38:32 GMT

The following headers would be valid
  x-ms-date = Thu, 30 Mar 2023 08:38:32 GMT
  x-ms-content-sha256 = lNlsp1XA03N34HrQsVzPgJKtC+r7l/RBF4V3JQUWMj4=
  Authorization = HMAC-SHA256 SignedHeaders=x-ms-date;host;x-ms-content-sha256&Signature=agAiSyogQbDHpeucoNwYz+yAr5nJ+v+zasdkSbqzv+U=
```

## Working C# sample code

```csharp
using System.Security.Cryptography;
using System.Text;

public class Examples
{
    [Fact]
    public void Verifying_Hmac_Headers()
    {
        var secret = "A0+AeKBRG2KRGvnNwJpQlb6IJFk48CKXCIcrLoHncVJKDILsQSxS6NWCccwWm6r6FhGKhiHTBsG2wo/xU6FY/A==";

        var requestUrl = new Uri("https://webhook.site/e2cee29b-012e-4f1d-8ef4-e95fd74a7a63");
        var actualContent = """{"some-unique-content":"ee6e441b-cc4a-46f8-895d-a5af79bcc233/hello-world"}""";
        var actualContentHash = "lNlsp1XA03N34HrQsVzPgJKtC+r7l/RBF4V3JQUWMj4=";
        var actualDate = "Thu, 30 Mar 2023 08:38:32 GMT";
        var actualAuthorization = "HMAC-SHA256 SignedHeaders=x-ms-date;host;x-ms-content-sha256&Signature=agAiSyogQbDHpeucoNwYz+yAr5nJ+v+zasdkSbqzv+U=";

        // Verify content hash
        var contentHashInBytes = SHA256.HashData(Encoding.UTF8.GetBytes(actualContent));
        var expectedContentHash = Convert.ToBase64String(contentHashInBytes);
        Assert.Equal(expected: expectedContentHash, actual: actualContentHash);

        // Verify signature
        var expectedSignedString = $"POST\n{requestUrl.PathAndQuery}\n{actualDate};{requestUrl.Authority};{actualContentHash}";

        using var hmacSha256 = new HMACSHA256(Encoding.UTF8.GetBytes(secret));
        var hmacSha256Bytes = Encoding.UTF8.GetBytes(expectedSignedString);
        var hmacSha256Hash = hmacSha256.ComputeHash(hmacSha256Bytes);
        var expectedSignature = Convert.ToBase64String(hmacSha256Hash);
        var expectedAuthorization = $"HMAC-SHA256 SignedHeaders=x-ms-date;host;x-ms-content-sha256&Signature={expectedSignature}";

        Assert.Equal(expected: expectedAuthorization, actual: actualAuthorization);
    }
}
```
</TabItem>
</Tabs>