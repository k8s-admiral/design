## Goals

Admiral strives to achieve these high level goals. Each page should define goals
to keep the design on track.

### Easy to Install

Admiral should be extremely easy to install. One comand to install or upgrade
admiral is a requirement.

### Clusters are Cattle

Admiral should manage as many resources as possible. There should be 1 resource
that is created by somthing other than Admiral which would be it's own
deployment. As stated in the previous goal this should also only be created by
the command line installer.

### CRUD/Rest APIs

Admiral should have a cohesive API layed out with standard REST practices.
Admiral's APIs should be document oriented and declarative not
functional/imperative.

### Concice Configuration

Configuration should remain in as few places as possible.

### Grok-able Configuration

Layers of configuration can get very complicated to understand and reason about.
It should be easy to understand where configuration came from and what the
resources will look like when created. This understanding must come before any
configuration is pushed to a source (like a repository).

### Secure and Auditable

Property sources should have at the very lease authn and auditability (like git
commits)

### Pluggable

Not all kubernetes installations/usecases are the same. Admiral should be
pluggable to enable more than just templating. This can get tricky with scope.
For now let's just say if a controller should do it Admiral should not.

### Event Driven

Admiral should avoid polling at all costs. This will help reduce overhead with
including Admiral.

### Monitorable

Let's add prometheus metrics.

### Integratable

Admiral should be built in a way that other services can integrate with it
easily (jenkins, github, kubectl)
