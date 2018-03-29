# OpenGDPR for Lawyers
Version 0.1.3

# Introduction
This summary document clarifies frequent legal discussions about the implementation of the OpenGDPR specification.

For more information about the spec, please refer to opengdpr.org.
Questions and Answers

## What is an Agent?  It's not a GDPR recognized role.
The Agent role was added by OpenGDPR and does not exist in the GDPR and is not a legal designation. It is a type of processor that supports the Controllers obligation to honor  Data Subject Requests by standardizing them into the OpenGDPR API format and by using the OpenGDPR APIs to distribute and track their status across many OpenGDPR-compliant processors.

## Why does the Agent forward requests but not callbacks?
The Controller can receive status updates themselves by adding a callback URL to their requests. All requests with callbacks will be updated when request status changes. If the Controller prefers to have the Agent collect and maintain status, they can leave off callback URLs and the Agent can add their own to maintain a record of the request’s current status.

## Who is liable if the Agent fails to distribute requests to Processors?
The Agent is liable. They have an agreement with the Controller to perform receipt and distribution of requests.


## Who validates that data subject requests have been honored (ie erasure)?
The DPA between the Controller and the Processor should define that the Processor must fulfill their obligations to honor requests they have received. The OpenGDPR tracks the request status. OpenGDPR does not include automatic verification that the Processors have honored the request.

## Do Controllers and Processors need an additional layer of DPAs to use OpenGDPR?
Maybe. It is likely that existing DPAs signed between the Controller and Processor will cover the use of the Agent. When Agents distribute requests to Processors, they are made on behalf of the Controller using the Controllers secure credentials. There is no additional layer of legal obligations between the Agent and additional Processors.

## Is an OpenGDPR Agent always a GDPR Processor?
Yes. In most cases the organization fulfilling the OpenGDPR role of Agent is also a processor of that Controllers data. It is possible for an organization to perform ONLY the OpenGDPR Agent role and perform no additional data subject processing. In this case, they are still legally a processor as they are processing data subject requests on behalf of the Controller

## Do Agents need to honor data subject requests?
Yes. Agents are legally Processors and as such they must honor data subject requests as defined in the GDPR.

## As a Processor, does receiving requests from an agent add to my GDPR exposure/risk?
No; Agents send requests using the authentication of the Controller. The requests are sent for the Controllers account and on behalf of the Controller. The Agent only sends requests when directed by the Controller. In practice the Processor may not know that requests originated from an Agent instead of a Controller. There is no explicit legal arrangement between the Agent and downstream processors. Any legal discussion around handling the data subject requests should be defined between the Controller and their Processors.
