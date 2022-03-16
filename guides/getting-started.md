# 🚀 Getting Started

## **Installation**

There are three methods for setting up a local Redwood node.

#### **Download from Github**

Pre-compiled binaries are available for all platforms (Mac, Linux, Windows) at [https://github.com/redwood/redwood/releases](https://github.com/redwood/redwood/releases). These binaries are built via Github Actions, although this does not guarantee that they are safe to use.

#### **Docker**

Docker images are available both for the Redwood node as well as the "static relay" node (see [the section on peer-to-peer communications](https://docs.redwood.dev/fundamentals/peer-to-peer-communications) to learn about relays).

First, install Docker with the [official instructions](https://docs.docker.com/engine/install/). Then, pull the image:

```shell
docker pull redwoodp2p/redwood
```

#### **Build from source**

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

## Running the node

**Regular binary**

****

**Docker**

To run Redwood in Docker, use the following command, making sure to replace `<local data dir>` with the location on the host machine where you wish to persist Redwood's configuration and data:

```
docker run -it \
        -p 21232:21231 \
        -v <local data dir>/config:/config \
        -v <local data dir>/data:/root/.local/share/redwood \
        -v <local data dir>/nurse:/nurse \
        redwoodp2p/redwood \
        /redwood -p /config/password.txt -c /config/.redwoodrc
```
