# 🌲 Redwood

Redwood is a **highly-configurable, distributed, realtime database** that manages a state tree shared among many peers. Imagine something like a Redux store, but distributed across all users of an application, that offers offline editing and is resilient to poor connectivity.

Redwood is also an **application server**. Developers can store and update assets (HTML, Javascript, images) directly in the state tree. For many types of applications, you may not need a separate backend server at all.

Its flexibility allows developers to use a single, simple programming model to create many divergent classes of applications:

* Traditional web applications
* Realtime collaborative document editors
* Peer-to-peer encrypted messaging
* Blockchains
* Git-style version control systems

## Getting Started

### Installing Redwood

There are three methods for setting up a local Redwood node.

**Download binary from Github**

Pre-compiled binaries are available for all platforms (Mac, Linux, Windows) at [https://github.com/redwood/redwood/releases](https://github.com/redwood/redwood/releases). These binaries are built via Github Actions, although this does not guarantee that they are safe to use.

**Build from source**

Requires Go 1.18. See the following resources to install Go:

* [https://go.dev/dl/](https://go.dev/dl/)
* [https://go.dev/doc/install](https://go.dev/doc/install)

Once Go is set up, run the following commands to clone the repository and build the Redwood binary:

```shell
git clone https://github.com/redwood/redwood
cd redwood/embed
yarn && yarn build
cd ../cmd/redwood
go build .
```

### Guides: Jump right in

Follow our handy guides to get started on the basics as quickly as possible:

{% content-ref url="guides/creating-your-first-project-vanilla-js.md" %}
[creating-your-first-project-vanilla-js.md](guides/creating-your-first-project-vanilla-js.md)
{% endcontent-ref %}

{% content-ref url="guides/creating-your-first-project-react.md" %}
[creating-your-first-project-react.md](guides/creating-your-first-project-react.md)
{% endcontent-ref %}

### Fundamentals: Dive a little deeper

Learn the fundamentals of MyProduct to get a deeper understanding of our main features:

{% content-ref url="fundamentals/what-is-a-state-tree.md" %}
[what-is-a-state-tree.md](fundamentals/what-is-a-state-tree.md)
{% endcontent-ref %}

{% content-ref url="fundamentals/subscriptions.md" %}
[subscriptions.md](fundamentals/subscriptions.md)
{% endcontent-ref %}

{% content-ref url="fundamentals/transactions.md" %}
[transactions.md](fundamentals/transactions.md)
{% endcontent-ref %}

{% content-ref url="fundamentals/merge-resolvers.md" %}
[merge-resolvers.md](fundamentals/merge-resolvers.md)
{% endcontent-ref %}

{% hint style="info" %}
**Good to know:** Splitting your product into fundamental concepts, objects, or areas can be a great way to let readers deep dive into the concepts that matter most to them. Combine guides with this approach to 'fundamentals' and you're well on your way to great documentation!
{% endhint %}
