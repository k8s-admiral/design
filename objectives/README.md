# Admiral Objectives

The number one objective of Admiral is to "Make managing multiple Kubernetes clusters
_easier_ and _simpler_ by utilizing _GitOps_". All other objectives/requirements
should funnel back to this goal.

## Easier

How much effort is required to use/install/debug/manage the service.

### Examples:

- Try to keep non git operations a one-liner in bash.
- Provide tools to debug systems locally.

## Simpler

Having a low complexity in the concepts that need to be learned before someone
can use Admiral effectively.

### Examples:

- Make sure high level concepts could be explained with a slide.
- Keep the number of concepts low.

## GitOps

Any operation that is able to be declarative should be able to happen through
changing configuration in git. Any Imperative operation should be _easy_.

### Examples:

- Merging into branches should be all that is _required_ to make changes to the
  system.
