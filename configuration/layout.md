# Config Layout

## /templates

Directory with helm templates or admiral templates

Subdirectories for each Kubernetes Resource Type

### Helm Templates

foo.helm.tmpl

### Admiral Templates

foo.tmpl

### Directory Structure Example

`templates/Deployment/foo.tmpl`

`templates/Service/standard/clusterIp.tmpl`

## /resourceGroups

An arbitrary directory structure with ResourceGroup files. All ResourceGroup
files have the `.rg.yml|.rg.yaml` extension. Where the name of the ResourceGroup
is the name of the full path to the file separated with dots.

`./foo/bar.rg.yml` file turns into the ResourceGroup name `foo.bar`

```yaml
vars: `Map<string, VarsMap | string | number | boolean>`
templates:
  <template-name>:
    type: `Kubernetes Object Type` # kubernetes object type
    path: `relativeTemplateURL | full URL git, ssh, http, file supported`
    vars: `Map<string, VarsMap | string | number | boolean>
```

## /clusters

Clusters holds a flat list of cluster configurations for admiral to manage where
the name of the cluster is the name of the file.

<!--prettier-ignore-->
> [!NOTE] 
> Auth and clusters might need to be separated.

<!--prettier-ignore-end-->

```yaml
server: `http url`
insecure-skip-tls-verify:
certificate-authority:
certificate-authority-data:
type: `cluster type`

# auth
client-certificate:
client-certificate-data:
client-key:
client-key-data:
token:
tokenFile:
act-as:
act-as-group:
act-as-user-extra:
username:
password:
auth-provider:
exec:
  command: `string`
  args: `args`
  env: `env`
```

## /namespaceTypes

namespaceTypes are templates for creating namespaces

```yaml
resourceGroups:
  <rg-name>:
    ref: `git ref`
    vars: `Map<string, VarMap | string | number | boolean>` # override vars
    createAfter:
      <rg-name>: `true | false`
```

## /clusterTypes

cluster types are templates for cluster level resources.

```yaml
resourceGroups:
  <rg-name>:
    ref: `git ref`
    vars: `Map<string, VarMap | string | number | boolean>` # override vars
```

## /plugins

```yaml
<plugin-name>:
  image: `docker image url` # plugin image url
  tag: `docker image tag` # plugin image tag (default: latest)
  timeout: `number` # max wait for plugin to respond
```
