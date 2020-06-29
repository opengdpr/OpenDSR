# OpenDSR Extensions

OpenDSR requests may contain an `extensions` object, composed of a series of child-objects, keyed by a processor domain.

- The domain of each extension **MUST** match the processor's OpenDSR domain.
- Extensions **MUST** not be used for or contain authentication information.
- Processors **MUST** only implement an extension for items that do not already fit into the generic spec.

See section the [OpenDSR spec](specification.md) for more information on the use of extensions.

## Published Extensions

### mParticle

Domain: `opendsr.mparticle.com`

Supported keys:

- `mpids`: An array of mParticle IDs. The mParticle ID is a 64-bit signed integer.
- `identities`: An array of additional mParticle-supported identity objects, each containing a key and value. Valid keys are:
  - `other`: mParticle ID `other`.
  - `other2`: mParticle ID `other2`.
  - `other3`: mParticle ID `other3`.
  - `other4`: mParticle ID `other4`.
  - `other5`: mParticle ID `other5`.
  - `other6`: mParticle ID `other6`.
  - `other7`: mParticle ID `other7`.
  - `other8`: mParticle ID `other8`.
  - `other9`: mParticle ID `other9`.
  - `other10`: mParticle ID `other10`.
  - `mobile_number`: mParticle ID `phone_number_1`.
  - `phone_number_2`: mParticle ID `phone_number_2`.
  - `phone_number_3`: mParticle ID `phone_number_3`.

### Example

```json
"extensions": {
    "opendsr.mparticle.com": {
      "mpids": [
        1234567890,
        5678901234
      ],
      "identities": [
        {
          "identity_type": "other1",
          "identity_value": "test@test1.com"
        }
      ]
    }
  }
```

### Schema

```json
{
  "type": "object",
  "properties": {
    "opendsr.mparticle.com": {
      "type": "object",
      "properties": {
        "mpids": {
          "type": "array",
          "items": {
            "examples": [
              120934871234,
              1309487143098
            ]
          }
        },
        "identities":{
          "type":"array",
          "items":{
            "examples":[
              {
                "identity_type": "example_type",
                "identity_value":"example_id_value"
              }
            ]
          }
        }
      }
    }
  }
}
```
