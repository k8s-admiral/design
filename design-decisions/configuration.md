# Configuration

## Where should Admiral store config?

Git repositories are great interfaces for storing configuration that come with
the following for free:

- Authentication
- Rudimentary Authorization
- History
- Backups (through distributed copies, and SaaS offerings)

Specifically history, and backups, are something that Kubernetes lacks. As much
information as possible should be stored in git. In the case of a loss of a
cluster, restoration should be as close as possible to creating a new vanilla
cluster and pointing admiral at it.

### Important Factors

- Config needs to be updated by a CD service.
- Config will need to be updated and read by a Human.

### Decision

A Git repository with yaml should be the main store for configuration. An
optional _Dynamic Variable Store_ (DVS) should be available via REST endpoints
on the Admiral API. The DVS should only hold Template Variables and refs. This
helps keep the purpose of the DVS focused and makes it easier to debug. DVS
should probably be a simple persistent key value store.

---

## How should the config be released?

Configuration should not be released to every cluster/namespace at the same
time. Generally in Continuous Delivery you want to release to one environment,
make sure everything is good, then move onto the next.

### Important Factors

- Releasing will generally be done with a CD service.
  - Git can be difficult for CD services.
- Releases should support lockstep releases as well as independent releases.
- Must scale to a large volume of releases.
- Versions of software should be independent of versions of configuration.

### Decision

When including Resource Groups a git ref can be provided either through the git
configuration, or the DVS. Admiral will checkout the ref of the configuration,
resolve the config, and push the results to kubernetes. Being able to use the
DVS for refs will be required for CD services because they are more imperatively
inclined.

### Examples

```bash
admiral set ref --cluster prod --namespace ingress --resource-group haproxy-ingress --ref release/prod
```

```yaml
haproxy-ingress:
  ref: master
  template: '...'
  vars: { ... }
```

---

## How do configuration dependencies work?

ResourceGroups could depend on each other. For instance if a ResourceGroup
needed a postgres instance to function it could have a dependency on a
ResourceGroup that deploys postgres. Generally speaking a service should be able
to run without it's dependencies even if it is in a less than optimal state.
However, this is not always the case, some services need to be up and available
before others deploy. Dependencies can solve this by providing a boot order, and
letting ResourceGroups define a BOM themselves.

### Important Factors

- Dependencies can cause confusion
- Circular dependencies can cause deadlocks
- Should ResourceGroups be able to depend on a particular ref/version of a
  ResourceGroup?

### Proposal

None

---

## How should inheritance work?

Inheritance in Namespace/Cluster Types allows managing multiple similar clusters
focus on what is different between them.

### Important Factors

- Needs to be easily understood
- Must provide flexibility for minor changes
- Avoid encouraging configuration that has to eventually be "cleaned up"

### Proposal

For both Cluster Types and Namespace Types an implicit root configuration is
found at the root folder.

File names should be arbitrary and all files in a directory merged into a single
configuration "layer".

The first layer should consist of large content differences. Layers following
the first should be minor changes that consist of the differences. This should
not be prescriptive in Admiral's interface, but rather, suggested as a "Best
Practice"

Lists should be not be used because they are difficult to merge.

```
clusterType/
|--build/
|  |--team1/
|  `--team2/
`--product/
   |--dev/
   `--prod/
      |--stage/
      |--beta/
      `--GA/

namespaceType/
|--ingress/
|--services/
|  |--dev/
|  `--prod/
|     |--stage/
|     |--beta/
|     `--GA/
`--build/
```

Then when configuring a cluster the cluster would reference a ClusterType in the
format of the folder e.g. `product/prod/stage`. When listing namespaces in a
cluster NamespaceTypes would be referenced similarly.

ClusterTypes/NamespaceTypes are implicitly infinite. Meaning any reference is
valid even if there is no configuration for it. For example, in the above file
structure one could reference a NamespaceType `service/prod/GA/us-east1` even
though there is no configuration for it. When merging configuration Admiral will
simply roll up configuration until nothing is found.
