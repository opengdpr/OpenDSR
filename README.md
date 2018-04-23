# OpenGDPR Summary
version 0.1.4

# Overview
This is an introductory document intended to provide a summary of OpenGDPR. For full reference details, please see the complete specification at https://www.opengdpr.org and https://github.com/opengdpr/opengdpr.

# Goals and Scope
The OpenGDPR specification defines a common approach for data Controllers and Processors to build interoperable systems for tracking and fulfilling Data Subject requests as defined under the General Data Protection Regulation (GDPR).

For more information on the Data Subject Rights, see chapter 3 of the GDPR.

This spec is intended to:
1. Provide a well defined JSON specification that allows Controllers and Processors to communicate and
manage Data Subject access, portability and erasure requests in a uniform and scalable
manner.
2. Provide strong cryptographic verification of request receipts to provide chain of
processing assurance and demonstrate accountability to regulatory authorities (Article
5.2).
3. Provide for a callback mechanism to enable Controllers to track the status of
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
**Data Subject**
A European Union resident whose personal data is being processed.

**Data Controller**
The Data Controller receives Data Subject requests from the Data Subjects and validates them. The Controller submits requests to the Data Processors.

**Data Processor**
The Data processor fulfills the request for the Controllers scope.

## Request Sequence
This diagram outlines the flow of GDPR data subject requests all the way from the data subject to the fulfillment by each Processor. This flow includes optional callbacks that allow the Controller to receive status changes.

![image](https://user-images.githubusercontent.com/566376/38212428-b4167bae-368b-11e8-8c1a-3d674083cd94.png)

1. New Data Subject Request: The data subject files a request to the data controller containing appropriate information. Request may be of any type provisioned in the GDPR text, commonly: access, portability, erasure, rectification.
2. Request Distribution: The controller verifies the request and if it will be honored, it is submitted to Processors.
3. Request Fulfillment: The Processor fulfills their obligation within the scope of this request. For example, this may include deleting user data in the case of a deletion request.
4. Request Status via Callback: The processor will submit status updates to the controller if callbacks are included in the request.
5. Communication to the Data Subject: The Controller communicates the results to the data subject.

## Request Types
The spec supports request types of “erasure”, "access" and “portability”. For all types, the details of how a processor fulfills the request is defined by the GDPR and is out of scope for this specification. For access and portability requests, secure transmission of the resulting personal data is left up to the controller and processor.

# API Summary
## Endpoints
This is an overview of available HTTP methods for communicating between Controllers and Processors. The following endpoints should be provided by the Processor (to receive requests from the Controller).

Restful API endpoints for the resource “opengdpr_requests”:

| HTTP Method | Path | Description | Supported? |
| --- | --- | --- | --- |
| POST | opengdpr_requests/ | Create a new OpenGDPR request | Yes |
| GET | opengdpr_requests/{RequestId} | Retrieve status of a single OpenGDPR request | Yes |
| PUT | opengdpr_requests/{RequestId} | - | No, requests cannot be updated after being created |
| DELETE | opengdpr_requests/{RequestId} | Cancel an OpenGDPR request | Yes, cancellation is valid in status “pending” only |

Non-Restful endpoints:

| HTTP Method | Path | Description | Supported? |
| --- | --- | --- | --- |
| GET     | /discovery | Processors describe their OpenGDPR support| Yes  |
| POST    | /callback | Sent by Processors when a request status changes| Yes |


#   Sample Request Object
Refer to the full specification for definitions of objects and fields.
```
{
 "subject_request_id":"a7551968-d5d6-44b2-9831-815ac9017798",
 "subject_request_type":"erasure",
 "submitted_time":"2018-10-02T15:00:00Z",
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
