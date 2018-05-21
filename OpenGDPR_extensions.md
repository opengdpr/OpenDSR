# OpenGDPR Extensions

OpenGDPR requests may contain an `extensions` object, composed of a series of child-objects, keyed by a processor domain. Extensions are defined here via markdown and JSON-Schema.

- The domain of each extension **MUST** match the processor's OpenGDPR domain.
- Extensions **MUST** not be used for or contain authentication information.
- Processors **MUST** only implement an extension for items that do not already fit into the generic spec.
- Extensions are namespaced by the processors OpenGDPR domain and have an explicit name/key.
- One processor may have many extensions under their namespace.

See section the [OpenGDPR spec](OpenGDPR_specification.md) for more information on the use of extensions.

# Extension Definitions
Extensions are defined in this document with the following fields:

- Domain: The OpenGDPR domain/subdomain for the processor publishing and consuming the extension.

- Name: The name of this extension.
Description: A brief description of this extension.

- Example in a new OpenGDPR Request: Show a snippet of how the extension should be used in an OpenGDPR request.

- JSON-Schema definition: A JSON-Schema snippet that defines the fields and formats expected by this extension.


---


# Published Extensions

## opengdpr.mparticle.com
### mpids

Domain: `opengdpr.mparticle.com`

Name: 'mpids'

Description:
  Provides support for passing mParticle's internal id "mpid" in a request.

#### Example in a new OpenGDPR Request

```json
...
"extensions": {
    "opengdpr.mparticle.com": {
      "mpids":[120934871234, 1309487143098]
    }
}
...
```

#### JSON-Schema Definition

```json
{
  "type": "array",
  "items":
  {
    "type":"64-bit signed integer",
  }
}
```
