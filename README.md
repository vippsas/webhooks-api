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

💥 Work in progress 💥

You can **subscribe** to published **event types** by registering webhooks and
will then be **notified** when any matching events are published that match the
given sales unit id.

As an example, a merchant can register a callback url to receive a callback when
any of the payments of the merchant is captured.

There is a set limit on how many registrations per event types per sales unit
allowed, see the API reference for the exact limit.

## Security

A notification request from webhooks can be verified using the following
headers, 'host', 'x-ms-date', 'x-ms-content-sha256' and 'authorization' with the
unique secret received when the webhook was registered. The authorization is a
sha256 HMAC hash of request date, content and uri that is created using the
webhook secret.

### Summary pseudo code
```cmd
let contentHash = hash(serializedContent)

let signatureText = POST\n{pathAndQuery}\n{date};{authority};{contentHash}
let signature = sign(secret, signatureText)
let authorization = HMAC-SHA256 SignedHeaders=x-ms-date;host;x-ms-content-sha256&Signature={signature}
```

### Sample values

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

### Working C# sample code

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