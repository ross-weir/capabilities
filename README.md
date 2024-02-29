# Capailities

## Overview

This repository contains my rough thoughts about an idea I have around a category of dApps.

Named "Capabilities" these dApps are designed to implement a specific piece of functionality and can be reused and composed to create complete dApps.

For example, a naming service would make heavy use a "Address Resolver" capaility but so could many other apps to convert addresses into names/handles.

By extension, there could also be "Capability groups" that combine commonly used together capabilities into a higher order capability - thus capabilities
are not only composable in dApps but also composable with each other. Such groupings could be made opaque so the fact the capability group is made up of many
capabilities it is still used in the same manner as individual capabilities.

## Capability development

Development, documentation and discussion of capailities will take place in a centralized monorepo. A possible layout could resemble:

```
capabilities
  name-resolution
    v1
      docs
        overview.md
        specification.md
        examples.md
        history.md
      cip
        cip-001.md
        cip-002.md
      contracts
        resolver.ral
        registry.ral
      metadata.json
  identity
    ...
  whitelist
    ...
CODEOWNERS.md
```

The usage of a centralized monorepo provides many benefits and should not be seen as centralization of development/control of development. It will allow for strong
collaboration, discoverability and documentation automation.

A team developing a name service are likely domain experts in name resolution. They have a vested interest in ensuring name resolution capabilities are of high standard.
`CODEOWNERS.md` could be used to allow such teams to have a bit more say in the direction of the capabilities they are interested in.

### docs

The `docs` directory would follow a strict/uniform structure and be stitched together to create a static website that contains a database of all provided capabilities.
This will be it easy for dApp developers to search for capabilities they might need in their dApp, easily view examples of capability usage, history of capability
development, specification of the capability, "similiar"/commonly used capabilities etc.

### cip (capability improvement proposals)

cips will live next to the code that they relate to. They will follow a strict structure/layout and will also be used in the static website geneartion to make
cips discoverable and facilitate discussion.

### metadata.json

The metadata file can contain general details about the capability, such as its identifier, tags (to group similar capabilites), current version, and any
other general metadata.

## usage

Capabilities could be used on a per-use-case basis but also could be provided conviently through a capability registry. So if your dapp needs to utilize many
capabilities you only need to refer to the capability registry and not many individual capabilities:

```
//...
let nameResolver = capabilityRegistry.getNameResolver("1.0.5")
let address = nameResolver.resolve(name)

....

let identity = capabilityRegistry.getIdentity("0.1.0")
identity.setProfilePicture(...)
//...
```

A very small fee could be charged for developers of the capability registry or developers can manage their capability usage directly if they desire.


## Considerations

- versioning and deprecation of capabilities. Each capability should be treated as a typical software library and follow versioning/deprecation best practices
    - to prevent onchain state bloat we may need to limit version history?

