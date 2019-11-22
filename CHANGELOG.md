Changelog
2.0
- Renamed this project 'OpenCompliance' to encompass CCPA support
- Changed references to OpenGDPR to OpenCompliance
- Added regulation field of 'regulation'
- Added section 10.1 to provide some guidance on supporting prior versions, including the renaming of the project
- Tagged V1 to branch `opengdpr_v1` for posterity: https://github.com/opengdpr/opengdpr/tree/opengdpr_v1

1.0
- Added support for `extensions`: processor-defined fields in each request. Used for additional scoping information (eg processor-project-id) or processor-specific identities (eg mparticle-id).
- Converted spec to markdown format for easier reading and editing.
- Added `results_url` to status objects to contain the outputs from an access or portability request when in status `completed`.
- Added versioning information and requirement to include major version in the OpenGDPR resource URL.

0.1.4
- Removed 'agent' role throughout and added a Best Practice to use a sub-processor to distribute requests and ensure mature infrastructure (retries, security verifications & logging)
- Removed 'GDPR for Lawyers' document that is no longer needed
- Removed IETF text at the top of the specification. This is a specification and not a standard so the IETF format is not needed.
- Corrected restful noun to "opengdpr_requests"
- Added status 'cancelled' as the ending status for cancelled requests
- Added versions to all API endpoints

0.1.3
- Update role descriptions of Agent as a type of processor and clarified agent responsibility to send callbacks when requests are distributed
- Updated flow diagram to include communication from controller to data subject
- Added status of 'distributed' to represent that an Agent has sent a request downstream to all parties.
- Clarified that this is a 'specification' and not a 'standard' nor a 'framework'
- Updated summary doc to match changes above
- Added an 'OpenGDPR for Lawyers' document aiming to clarify frequent legal questions about OpenGDPR

0.1.2
- Changed ‘broker’ to ‘agent’ throughout
- Renaming controller/processor to ‘data controller’ / ‘data processor’  in roles section
- Added several gdpr citations for chapters / articles
- Added Aurelie (mParticles DPO) as a contributor to the bottom
- Added HTTP DELETE method for cancellation if request is in ‘in progress’ status
- Clarified that processors only MUST try to send callbacks once and recommended but not required to retry
- Added “property_id” field to request
- Added “client_customer_id” to identity support list
- Added “supported_subject_request_types” field to discovery
- Added a request types of “portability” and “access”. No other changes specific to these request types have been made.
