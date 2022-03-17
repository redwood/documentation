# ⚙ Configuration

## System configuration

### IPv6

Configuring IPv6 is likely to improve your node's connectivity with other nodes, as long as they're configured to use it as well.

#### Linux

If you are running Redwood as a simple binary (as opposed to within a Docker container) on a Linux machine, the process is straightforward.

First, add the following lines to `/etc/sysctl.conf`:

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
```

Then, run the following command to activate your changes:

```
sysctl -p
ip6tables -t nat -A POSTROUTING -s fd00::/80 ! -o docker0 -j MASQUERADE
```

#### Docker

If the node is running within a Docker container, two additional steps are required. Create a file called `/etc/docker/daemon.json` containing the following:

```json
{
    "ipv6": true,
    "fixed-cidr-v6": "fd00::/80"
}
```

Then, run the following command to activate your changes:

```
systemctl restart docker
```

## Redwood configuration

When Redwood starts for the first time, it will create a configuration file called `.redwoodrc` in the location you specified with the `-c` (or `--config`) flag. It's recommended that you stop Redwood and investigate this file to ensure that your node is configured as you wish.

`.redwoodrc` is a YAML file with the following structure:

```yaml
DataRoot: ~/.local/share/redwood
BootstrapPeers:
  - Transport: libp2p
    DialAddresses:
      - /ip4/192.168.0.120/tcp/21241/p2p/16Uiu2HAmQi6fqAoBxjqSB6xZ8fsiN6YpDhn4W3crVVnQaGctBhsT
  - Transport: braidhttp
    DialAddresses:
      - https://xyzzy.org:8080
DNSOverHTTPSURL: ""
JWTSecret: asf98j234f8jpwksdjf09230fjksadjfklajslkdfj90

#
# Protocols
#
AuthProtocol:
    Enabled: true
BlobProtocol:
    Enabled: true
HushProtocol:
    Enabled: true
TreeProtocol:
    Enabled: true
    MaxPeersPerSubscription: 4

#
# Transports
#
Libp2pTransport:
    Enabled: true
    ListenAddr: 0.0.0.0
    ListenPort: 21231
    Reachability: ""
    ReachableAt: ""
    StaticRelays: []
BraidHTTPTransport:
    Enabled: true
    ListenHost: :8080
    ListenHostSSL: :8082
    TLSCertFile: ""
    TLSKeyFile: ""
    DefaultStateURI: chat.com/room-2837
    ReachableAt: http://localhost:8080

#
# Insecure RPC endpoint
#
HTTPRPC:
    Enabled: true
    ListenHost: :8081
    TLSCertFile: ""
    TLSKeyFile: ""
    Whitelist:
        Enabled: false
        PermittedAddrs: []

#
# Debugging/profiling
#
PprofPort: 6060
Nurse:
    Enabled: false
    ProfileRoot: /tmp/redwood-pprof
    PollInterval: 10s
    GatherDuration: 10s
    MaxProfileSize: 100.00mb
    CPUProfileRate: 1
    MemProfileRate: 1
    BlockProfileRate: 1
    MutexProfileFraction: 1
    MemThreshold: 5.00gb
    GoroutineThreshold: 10000

```
