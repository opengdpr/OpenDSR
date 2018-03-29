# OpenGDPR Summary
version 0.1.3

# Overview
This is an introductory document intended to provide a summary of OpenGDPR. For full reference details, please see the complete specification at https://www.opengdpr.org and https://github.com/opengdpr/opengdpr.

# Goals and Scope
The OpenGDPR specification defines a common framework for data Controllers and Processors to build interoperable systems for tracking and fulfilling Data Subject requests as defined under the General Data Protection Regulation (GDPR).

For more information on the Data Subject Rights, see chapter 3 of the GDPR.

This spec is intended to:
1. Provide a well defined JSON specification that allows Controllers and Processors to communicate and
manage Data Subject access, portability and erasure requests in a uniform and scalable
manner.
2. Provide strong cryptographic verification of request receipts to provide chain of
processing assurance and demonstrate accountability to regulatory authorities (Article
5.2).
3. Provide for a callback mechanism to enable Controllers to identify the status of
all Data Subject requests.

This specification does not cover:
1. Defining the technical measures to describe the fulfill of Data Subject requests.
It is the responsibility of each Data Controller and Data Processor to interpret and
apply the GDPR to honor Data Subject requests (GPDR Chapter 3).
2. The protocol for communications between Controllers and Data Subjects.
3. The protocol for communications between Controllers, Processors and Supervisory
Authorities.
4. The protocol for communication of the results of an access or portability request.



# Roles and Request Lifecycles

## Roles
**Data Controller**
The Data Controller receives Data Subject requests from the Data Subjects and validates them. The Controller submits requests to the Agent for distribution to Data Processors.

**Data Processor**
The Data processor fulfills the request for the Controllers scope.

**Agent**
An Agent is a type of Data Processor that accepts requests and federates them to one or many Data Processors as directed by the Controller.


## Request Sequence
This diagram outlines the flow of GDPR data subject requests all the way from the data subject to the fulfillment by each Processor. This flow includes optional callbacks that allow the Controller or Agent to receive status changes.

![image](https://user-images.githubusercontent.com/566376/38100987-f73ca274-334c-11e8-93d1-fde0236e8bd0.png)

1. New Data Subject Request: The data subject files a request to the data controller containing appropriate information. Request may be of any type provisioned in the GDPR text, commonly: access, portability, erasure, rectification.
2. Request Submission:  The controller verifies the request and if it will be honored, it is submitted to the Agent. The controller directs which processors receive each request.
3. Request distribution: The request agent submits the request to each processor as directed by the controller.
4. Request Fulfillment: The Processor fulfills their obligation within the scope of this request. For example, this may include deleting user data in the case of a deletion request.
5. Request Status via Callback: The agent will submit status updates to the controller if included in the request or injected by the agent.
6. Request Status via Callback: The agent will propagate callbacks as necessary to pass status back to the controller.
7. Request Status via Callback: The processor will submit status updates to the controller and agent if included in the request.
8. Communication to the Data Subject: The Controller communicates the results to the data subject.

## Request Types
The spec supports request types of “erasure”, "access" and “portability”. For all types, the details of how a processor fulfills the request is defined by the GDPR and is out of scope for this specification. For access and portability requests, secure transmission of the personal data is left up to the controller & agent.

# API Summary
## Endpoints
This is an overview of available HTTP methods for communicating between controllers, agents and processors. The following endpoints should be provided by the agent (to receive requests from controllers) and processor (to receive requests from the agent).

Restful API endpoints for the resource “opengdpr_requests”:

| HTTP Method | Path | Description | Supported? |
| --- | --- | --- | --- |
| POST | opengdpr_requests/<RequestId> | Create a new OpenGDPR request | Yes |
| GET | opengdpr_requests/<RequestId> | Retrieve status of a single OpenGDPR request | Yes |
| PUT | opengdpr_requests/<RequestId> | - | No, requests cannot be updated after being created. |
| DELETE | opengdpr_requests/<RequestId> | Cancel an OpenGDPR request | Yes, cancellation is valid in status “pending” only |


Non-Restful endpoints:

| HTTP Method | Path | Description | Supported? |
| --- | --- | --- | --- |
| GET     | /discovery | Processors and Agents describe their OpenGDPR support| Yes  |
| POST    | /callback | Sent by Processors and Agents when a request status changes.| Yes |


#   Sample Request Object
Refer to the full specification for definitions of objects and fields.
```
{
 "subject_request_id":"a7551968 d5d6 44b2 9831 815ac9017798",
 "subject_request_type":"erasure",
 "submitted_time":"2018 10 02T15:00:00Z",
 "subject_identities":[
   {
      "identity_type":"email",
      "identity_value":"johndoe@example.com",
      "identity_format":"raw"
   }
 ],
 "api_version":"0.1",
 "property_id":"123456",
 "status_callback_urls":[
   "https://example controller.com/opengdpr_callbacks"
 ]
}
```
