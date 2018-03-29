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
