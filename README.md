# Admiral

Admiral is a configuration management system for Kubernetes using git-ops. Right
now it is in the design stages. This repository is intended to serve as a place
to set that design before any code is written. Configuration management is
sensitive with a lot of considerations. While feature bloat should be avoided
the first version of Admiral should be complete enough to define it's scope and
be useful.

## Basic Design

A git repository will house three types of configuration. This configuration
will be combined to form Kubernetes resources and sent to Kubernetes through the
Kubernetes API Server.

### Resource Templates

Resource templates are simply yaml files with a templating syntax used to
manipulate differences between various uses of Kubernetes resources. As an
example a Deployment yaml template could have a template syntax for the value of
the `image` key and multiple Deployments could be created by changing the image
of the pod container.

### Resource Groups

Resource Groups combine several Resource Templates and variables for those
templates into an atomically deployable group. These are like a helm chart
except templates are referenced in Resource Groups rather than included with
them.

### Namespace/Cluster Types

Namespace and Cluster Type are layered configuration that acts as a "Bill of
Materials" for a Namespace and it's namespaced resources or a Cluster and it's
cluster wide resources. The configuration is "layered" to act as an inheritance
model. This way many clusters/namespaces can have slight variations in
Configuration, Bill of Materials, and Release Cadence while keeping
configuration _DRY_.
