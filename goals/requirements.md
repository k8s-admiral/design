## Versionable Configuration

A single source of config should be able to manage all clusters in a given
armada. Even if some clusters are just different stages of the same deploy. This
means the configuration needs to be versionable. Or Admiral needs to be able to
reference a version when pointing to an EnvironmentType

## Grok-able, Concise Configuration

Layers of configuration can get very complicated to understand and reason about.
It should be easy to understand where configuration came from and what the
resources will look like when created. This understanding must come before any
configuration is pushed to a source (like a repository).
