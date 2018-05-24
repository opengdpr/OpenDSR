# Security Guidelines
Security guidelines to jumpstart implementations and avoid security pitfalls.

## Certificates
1. Purchase certificate solely for OpenGDPR to prevent issues elsewhere with your infrastructure if
you ever need to revoke your OpenGDPR certificate for any reason.
2. Certificate must be purchased for a dedicated OpenGDPR subdomain rather than using a wildcard
or subdomain that is use for other purposes. We recommend following the standard form of
opengdpr.companydomain.com, for example: opengdpr.mparticle.com
3. Valid CA signed certificates should be mandated where possible and self signed certificates should
be avoided for this purpose to allow other parties to validate your certificate is valid.
4. Preferably obtain an EV certificate to provide increased verification of company association.

## Callback validation:
All callbacks must be issued over TLS, and the server certificate must be validated to match the callback
endpoint.
1. It is recommended that controllers maintain a whitelist of processor domains allowed to issue
callbacks. If such a whitelist is not kept, any entity with a valid certificate will be able to send data to
the controller’s callback endpoints. When a callback is received, the controller should validate that
the processor’s domain (taken from the X­OpenGDPR­Processor­Domain header) is in the
processor whitelist.
2. If the processor’s domain is in the whitelist, the certificate must be validated before checking the
signature:

     1. Callback issuers must publish their signing certificate on the /discovery endpoint of their OpenGDPR domain
          i. This certificate may be cached for the lifetime of the certificate
     2. Validate that the certificate hasn’t expired
     3. Validate that the certificate was issued by a trusted CA
     4. Validate that the certificate hasn’t been revoked
     5. If the certificate has been revoked and it was cached, the controller should retry by downloading the certificate from /discovery
     6. Validate that the processor’s domain is in the certificate’s SAN
     7. Validate that the certificate has the ‘Data Signature’ extension
Steps ii through vi should be handled by a library and not validated manually.

3. If the certificate is valid, the signature (taken from the `X-OpenGDPR-Signature` header) must be validated:
     1. Extract the public key from the processor’s certificate
     2. Validate the base64-decoded signature against the raw request body using the SHA256 digest.

4. If both the certificate and signature are valid, the payload can be processed:
     1. Base64 decode the callback body
     2. Validate that it is valid JSON
     3. Process the callback

5. Respond to the callback.
     1. The endpoint must return a 202 Accepted if:
          * All validations succeeded
     2. The endpoint must return a 401 Unauthorized if:
          * The processor domain is not in the whitelist
          * The certificate fails to validate
     3. The endpoint must return a 400 Bad Request if:
          * The signature is not valid
          * The payload is not valid JSON
