# Admiral Goals

The number one goal of admiral is to "Make managing multiple Kubernetes clusters
easier and simpler by utilizing git ops". All other goals/requirements should
funnel back to this goal.

## Easier

Easier refers to how much effort is required to use/install/debug/manage the
service.

## Simpler

Simpler refers to having a low complexity in the number of things that need to
be learned before someone can be effective with the tool.

It also refers to how quick an issue can be debugged.

K8s Admiral should have as few caveats as possible. All caveats should be well
documented and be able to be contained in a single head space (should understand
all applicable caveats for a given task without having to look up
documentation).

## Git-Ops

Any operation that is able to be declarative should be able to happen through
changing configuration in git. Any Imperative operation should be _easy_ through
a one liner `curl` command.

## Sub Goals

Each sub goal should have some sort of objective result or key metric it's based
on.

### Adoption

Adoption is a huge driver behind design decisions. Adoption should be the
fallback goal in any case where a design decision does not affect other goals.

#### Metrics

- Stars on GitHub
- Unique homepage visits per day
- Number of issues created

#### Ideas for achievements

- Social media engagement, announcement posts, blog articles, etc.
- Talks at tech conferences.
- Compatibility with existing eco systems (helm charts).
- Developed in a familiar language (golang).
- Ecosystem engagement. (provide a useful resource like a helm chart search /
  central repository)

### Compatibility

The biggest barrier to adoption is having to throw everything you have already
created out. Being compatible with an existing ecosystem means our ecosystem is
large at launch.

#### Metrics

- Automated test cases

#### Ways to achieve

- Work with helm chart templates
  - by re-implementing the same template system.
  - by running helm background process and caching results.
  - by importing helm as a golang library (only feasible with golang).
- Work with yaml, or other well supported existing config language so we don't
  have to write a bunch of tooling.

### Contribution

Getting good developer contribution is a sign that adoption is increasing. If we
want that to be a good reflection of people using it we need to have a low
barrier to entry for developers who already work with kubernetes technologies.

- Developer experience should be intuitive
- good code structure/documentation.
- Might need to be written in golang to get developer engagement.

### Performance and Scalability

Making sure everything is event driven can help with this. Appropriate threading
is going to be critical. An event look implementation is probably a good idea.

#### Metrics

- Number of clusters able to manage.
- High latency situations.
- Number of object per cluster.
- Template inflations per second.
- Size of templates.
- Size of configuration repo able to process.

### Security

Should allow basic auth, and at least two external authorization strategy for
instance Kubernetes service accounts, OpenID connect, or other JWT
authentication methods. Having at least 3 methods of authentication will force
an authentication strategy.

Some form of ACLs should be implemented for all imperative actions.

### Auditability

All imperative actions (including configuration updates) should have an
accessible and exportable audit log.

### Integratable

Should be easy to integrate into existing systems/workflows/CI/CD platforms

This means tools should be simple and easy to install. It should be very easy to
interact with admiral with a bash script. This being the lowest common
denominator for pretty much everything.

### Pluggable

Not all Kubernetes installations/use cases are the same. Admiral templating
should be pluggable to enable more than just standard templating. This can get
tricky with scope. For now let's just say if a controller should do it Admiral
should not.

Loading random plugins invites security problems. This should be taken into
consideration.

- This is a big issue for golang, making golang pluggable is not idiomatic.
  - subprocess plugins could work.
    - subprocess plugins would mean a theoretical increase in flexibility in
      that something like bash could be a plugin language.
    - In reality golang is the only legitimate contender for creating an easily
      distributable/mountable subprocess.
  - API service plugins could be a thing but I think that breaks the
    [Simpler](#simpler) goal.
- If it is done in typescript a javascript or even typescript plugin would be
  incredibly easy.

### Funding

#### Options

- Support has worked for a lot of companies but can become a conflict of
  interest. Docs and do it yourself support will by necessity suffer.
- Feature Bounties, again are a conflict of interest. If the funding stops the
  contribution will suffer. And the ability for other people to contribute will
  need to be reduced to ensure the maintainers can be paid for work.
- Enterprise features has seemed to work really well. Saas features provided on
  top of the open source features would be a great way to get paid. It also
  makes sure that the CAC ratio for customers is high. Only large companies will
  want to pay so there would be few customers.
