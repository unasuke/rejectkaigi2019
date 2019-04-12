# OCI-compatible haconiwa
subtitle
: ─ hurdles and advantages ─

subtitle
: 2019-04-12

subtitle
: RejectKaigi 2019 @ pixiv Inc

author
: Yusuke Nakamura (unasuke)

theme
: unasuke-white

# about me
- Yusuke Nakamura (also known as "unasuke")
  - Employee of BANK Inc
    - Develop Rails application, manage Infrastructure <https://cash.jp/>
  - RubyKaigi 2019 helper
  - {::tag name="x-small"}GitHub [@unasuke](https://github.com/unasuke){:/tag}
  - {::tag name="x-small"}Twitter [@yu\_suke1994](https://twitter.com/yu_suke1994){:/tag}
  - {::tag name="x-small"}Mastodon [@unasuke@mstdn.unasuke.com](https://mstdn.unasuke.com/@unasuke){:/tag}

![](img/icon_raw.jpg){:relative_width="24" align="right" relative_margin_right="-9" relative_margin_top="42"}

# introduction
First, to clearly where we stand.

# Your perception of containers
- Are you use container?
  - In production env? or(and) development env?
  - Use Docker? or the other one?
  - Orchestrate by ECS? or GKE? or on-premises?

# We use Docker mostly
- de facto standard of a Linux container
  - Easy installation
    - for Mac, for Windows...
  - The first famous Linux container inplementation

# "Container" is not equal "Docker"
- Before Docker
  - LXC (Linux)
  - Jail (FreeBSD)
  - etc...
- After Docker
  - cri-o
  - Kata Container
  - etc...

# What's haconiwa
- The Linux contianer runtime written by C and mruby
  - <https://speakerdeck.com/udzura/the-alternative-container?slide=11>
  - > OCIのspecを必ずしも満たすことは想定していない
  - Independent from "Container" world
    - "Container" means OCI

# What's OCI
The initialism of "Open Container Initiative"

<https://www.opencontainers.org/>

- OCI specs
  - Image spec
    - specifitation of the container image format
  - Runtime spec
    - specification of the container runtime interface


# CRI and Kubernetes world
![](https://d3vv6lp55qjaqc.cloudfront.net/items/0I3X2U0S0W3r1D1z2O0Q/Image%202016-12-19%20at%2017.13.16.png){:relative_width="95"}

- kubelet uses Container-Runtime-Interface(CRI) to communicate to container runtime
  - > The kubelet is the primary “node agent” that runs on each node.

# Diff of OCI/CRI compatible means...
- CRI compatible
  - usable as backend of kubelet
- OCI compatible
  - Exchangeable image and runtime

\\n
easy → CRI compatible → OCI compatible → hard

# Why CRI-compatible?
haconiwa is just run container. Doesn't orchestrate.

- Pros
  - Orchestration by Kubernetes
- Cons
  - Cannot use haconiwa-specific functions (hook)
    - maybe...

# Why OCI-compatible?
- Pros
  - possible to share the existing assets
    - hub.docker.com
- Cons
  - Cannot use haconiwa-specific functions (hook)
    - https://github.com/haconiwa/haconiwa/blob/master/sample/hooks.haco
    - maybe...

# hurdles and advantages
- hurdles
  - it's hard to comply with the standard
- advantages
  - more users
  - wealth of existing assets

# How to implement CRI
<https://github.com/kubernetes/kubernetes/blob/release-1.14/pkg/kubelet/apis/cri/runtime/v1alpha2/api.proto>

- Protocol Buffer
  - RuntimeService
  - ImageService
  - and many messages
- middleware?

# CRI interface and haconiwa
- should start process to respond rpc
  - currently, haconiwa is just a command not service(or daemon)
- should implement rpc response interface

# OCI specification and haconiwa
- image spec
  - should import/export OCI image
  - <https://blog.unasuke.com/2018/read-oci-image-spec-v101/>
- runtime spec
  - <https://udzura.hatenablog.jp/entry/2016/08/02/155913>

# conclusion
- more resources, more users in OCI/CRI world
- but...
  - compliant to CRI is hard
  - compliant to OCI is harder than CRI

# conclusion
![](img/oci-tweet.png){:relative_width="95"}

<https://twitter.com/yu_suke1994/status/1068355444928741376>
