# Admiral Property Sources

define many resources with type of PropertySource and reference them in the
Armada Resource.

```yaml
type: k8s-admiral.dev/PropertySources
spec:
  priority: 1 # lower is higher priority. should fail on diplicate numbers.
  updateStrategy: x # move strat here. should be polling or webhook. webhook is not configurable.

  git:
    branchFilter: master # javascript regex
    url: ssh://git@github.com # some sort of nodegit compatible url
    credentials: xxx # can use a secret or just inline them?
    updateStrategy: # something about polling, on every request, or webhook, admiral can even generate the webhook and stick it in the resource for you.
  database:
    url: #sql url
    dialect: # postgres/mysql/etc
    credentials: # secret or not
  url:
    url: # generic url that you can just curl and get some form of json back from. Must be https?
    credentials: # secret reference
    certs: #?
  vaultdb:
    # not sure what config needs to be here
  mongo:
    # idk the sky's the limit i guess?
  rest:
    namespace:
    service:
    port:
    certs:
    path:
```

Then in the
[armada document](https://notes.fromnibly.com/St3djonSQvqoWwjRE4cqfw) the armada

create endpoints to show raw properties, structured properties, and to inflate a
template.
