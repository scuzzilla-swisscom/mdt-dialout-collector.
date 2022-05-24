### MDT aka Model Driven Telemetry

[YANG](https://datatracker.ietf.org/doc/html/rfc6020) is the data modeling language chosen by the Telco industry to represent
network devices' configurations and states.

The data, modeled using YANG, is gathered _(or sent)_ from _(to_) the devices over the network using protocols like
[NETCONF\/RESTCONF](https://datatracker.ietf.org/doc/html/rfc6241) and typically encoded using JSON or XML. The data sent/received
via NETCONF is usually going over SSH (or, more generic, TLS).

Around five years ago, Google srated working on a new RPC framework called [gRPC](https://www.grpc.io) which is now adopted by
all the main Vendors to retrieve/send data to the network. The most famous implementation are [gNMI](https://github.com/openconfig/gnmi)
and [gRPC Dial-in\/Dial-out](https://xrdocs.io/telemetry/blogs/2017-01-20-model-driven-telemetry-dial-in-or-dial-out/)

### gRPC vs NETCONF _short version_

- gRPC is generally faster to develop with: it's using [Protocol Buffers](https://developers.google.com/protocol-buffers/) as the
Interface Description Language and an ad-hoc compiler to automagically generate the associated code.

- gRPC is out-of-the-box supporting multiple programming languages and gives you the freedom to choose the one which fits best your skills
independently from the existing implementations (the Protobuff file is pre-defining the specs for both client and server).

- gRPC is efficient and scalable: it's taking advantage of the efficiency coming from [HTTP/2](https://datatracker.ietf.org/doc/html/rfc7540)
and thanks to Protocol Buffers, the transit data is binary encoded which considerably reduces the message size.

### gRPC Dial-in vs gRPC Dial-out vs gNMI _short version_

gNMI (gRPC Network Management Interface) is using the gRPC framework and a [standardized Protobuff](https://www.openconfig.net/projects/rpc/)
file to implement a solution to fully operate the network.

With what concerning gRPC dial-in/dial-out The data-stream is always pushed-out from the router, however in case of Dial-in the connection
is initiated by the collector, vice-versa with Dial-out the connection is initiated by the router.
The biggest benefit of Dial-in over Dial-out is that you're gonna have a single channel usable for both telemetry & routers configuration.

---

### MDT Dial-out collector

The main aim of this project it to use the gRPC framework to implement a multi-vendor gRPC Dial-out server. Currently the application is implementing
both the [Cisco's gRPC Dial-out .proto file](https://github.com/ios-xr/model-driven-telemetry/blob/ebc059d77f813b63bb5a3139f5178ad11665d49f/protos/66x/mdt_grpc_dialout/mdt_grpc_dialout.proto)
and the [Huawei's gRPC Dial-out .proto file](https://support.huawei.com/enterprise/en/doc/EDOC1100139549/40577baf/common-proto-files).

With the limits imposed by Vendors implementations, both JSON and GPB-KV are supported.

| Vendor | OS Version  |   Encoding   |
|--------|-------------|--------------|
| Cisco  | XR (...)    | JSON, GPB-KV |
| Cisco  | XE (...)    | GPB-KV       |
| Huawei | VRP (...)   | JSON, GPB-KV |












