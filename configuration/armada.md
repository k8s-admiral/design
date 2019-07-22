# Armada

This defines configuration for the admiral to direct the armada.

Because this and some other configuration shouldn't be managed by the running
k8s-admiral we should make an easy way to back it up and push it to a cluster to
get going.

```yaml
spec:
  clusters:
  - masterUrl:
    isHome:
    certificate:
      # should trust? certificate data?
    credentials:
      token:
      username:
      password:
      oauthStrategy:
      etc:
```

## isHome

self upgrade? self upgrade could be complicated but it would make things easier
for the operator (as long as it always works.)
