# Resource Group

## k8s resource

Should admiral create resources to express it's current status?

```yaml
status:
  templates: # what about name collisions?
    - type: Deployment
      templateURL: x
      vars: {}
```

## config

```yaml
resourceGroups:
  <name>:
    dependencies:
      <name>: "boot/runtime/optional"
    templates:
```

### dependencies

#### boot

Will be created and wait for ready before creating this resource.

#### runtime

Will be included in the list of resourceGroups. will be created and wait for
ready before marking the environment ready.

#### optional

will provide status that this is missing if it was not included

What are the implications of this? will this just create mismatches?

what about dependencies in another environment?
