# OpenGDPR Extensions

OpenGDPR requests may contain an `extensions` object, composed of a series of child-objects, keyed by a processor domain. Processors **MUST** only implement an extension for items
that do not already fit into the generic spec. Extensions **MUST** not be used for or contain authentication information. 

Example use cases are:
- processor-specific user/device ids
- additional non-sensitive metadata

```json
"extensions": {
    "example-processor.com": {
      "foo-processor-custom-id":123456
    },
    "example-other-processor.com": {
      "another-custom-key":"baz"
    }
}
```

## Published Extensions

### mParticle

Domain: `opengdpr.mparticle.com`

Supported keys:

- `mpid`: The internal mParticle ID. This is a 64-bit integer. Due to JSON library rounding, it's recommended to send this is a string.

### Example

```json
"extensions": {
    "opengdpr.mparticle.com": {
      "mpid":"120934871234"
    }
}
```