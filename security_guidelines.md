# Security Guidelines
Security guidelines to jumpstart implementations and avoid security pitfalls.

## Certificates
- Purchase certificate solely for OpenGDPR to prevent issues elsewhere with your infrastructure if
you ever need to revoke your OpenGDPR certificate for any reason.
- Certificate must be purchased for a dedicated OpenGDPR subdomain rather than using a wildcard
or subdomain that is use for other purposes. We recommend following the standard form of
opengdpr.companydomain.com, for example: opengdpr.mparticle.com
- Valid CA signed certificates should be mandated where possible and self signed certificates should
be avoided for this purpose to allow other parties to validate your certificate is valid.
- Preferably obtain an EV certificate to provide increased verification of company association.

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

  a. Callback issuers must publish their signing certificate on the /discovery endpoint of their OpenGDPR domain
    i. This certificate may be cached for the lifetime of the certificate
  b. Validate that the certificate hasn’t expired
  c. Validate that the certificate was issued by a trusted CA
  d. Validate that the certificate hasn’t been revoked
  i. If the certificate has been revoked and it was cached, the controller should retry by downloading the certificate from /discovery
  e. Validate that the processor’s domain is in the certificate’s SAN
  f. Validate that the certificate has the ‘Data Signature’ extension
Steps b through f should be handled by a library and not validated manually.

3. If the certificate is valid, the signature (taken from the X­OpenGDPR­Signature header) must be validated:
  a. Extract the public key from the processor’s certificate
  b. Validate signature against the base64 decoded request body

4. If both the certificate and signature are valid, the payload can be processed:
  a. Base64 decode the callback body
  b. Validate that it is valid JSON
  c. Process the callback

5. Respond to the callback.
  a. The endpoint must return a 202 Accepted if:
    i. All validations succeeded
  b. The endpoint must return a 401 Unauthorized if:
    i. The processor domain is not in the whitelist
    ii. The certificate fails to validate
  c. The endpoint must return a 400 Bad Request if:
    i. The signature is not valid
    ii. The payload is not valid JSON
