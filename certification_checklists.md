## Overview
As an open-source project, there is no centralizing body that can assess if implementations of OpenGDPR are following the spec correctly. Instead  implementors can self-certify their implementation by testing it against the following two checklists, one for processors and one for controllers.

## Self-Certification Checklist: Processors

- [ ] New requests: validations and correctly processing new requests, including included extensions
- [ ] Request status objects: sending correct status objects and `expected_completion` time
- [ ] Request cancellation
- [ ] Generating and securing results files in the `results_url` field
- [ ] `/discovery`: public certificate, supported identity types, extensions
- [ ] API security: authentication & authorization
- [ ] Requests are signed with the private key
- [ ] Private key is protected and securely managed
- [ ] Callbacks are sent on status changes
- [ ] Major version number in URLs
- [ ] Logging activity
- [ ] Publishing any required extensions
- [ ] Defined process for fulfilling each request type
- [ ] Metrics on the fulfillment to ensure correct operations


## Self-Certification Checklist: Controllers
- [ ] New `opengdpr_requests`: correctly populating required fields especially  `identity_types` and `extensions`
- [ ] Request status: polling or callbacks to track progress
- [ ] Callback receipt: stable endpoint for receiving status objects
- [ ] Certificate validation and caching
- [ ] Signature validations on requests
- [ ] Logging
