# Language Choices

## Kotlin (JVM)

Pros:

- Can be fast if you are good.

Cons:

- High memory footprint (jvm)
- Slow boot
- Java
- Not as common as golang in Kubernetes/Ops in general

## Typescript (Node.js)

Pros:

- Perfect for highly paralellizable tasks
- Generics which can be good for plugins
- Plugins can just be a typescript file
- Really easy REST servers

Cons:

- Slower at computational tasks (template inflation).
  - Though it can just use helm as a subprocess.
- Not as common as golang in Kubernetes/Ops in general.
- Kubernetes client library is not as polished.

## Golang

Pros:

- Could (maybe) work with helm as a library instead of a subprocess.
- High adoption rate in Kubernetes/Ops in general.
- Fast!!!
- Best Kubernetes Client (though there are no generics!)

Cons:

- Explicit parallelization.
- Plugins would be hard. https://golang.org/pkg/plugin
  - No generics.
  - Hard to test in isolation?
- I'm not as familiar with golang.
