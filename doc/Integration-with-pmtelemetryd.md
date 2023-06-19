```SHELL
$ doas cat /etc/os-release

PRETTY_NAME="Debian GNU/Linux 11 (bullseye)"
NAME="Debian GNU/Linux"
VERSION_ID="11"
VERSION="11 (bullseye)"
VERSION_CODENAME=bullseye
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
```

## Compile/Install gRPC dial-out library/Header for pmtelemetryd

```SHELL
$ sudo /bin/sh -c "$(curl -fsSL https://github.com/network-analytics/mdt-dialout-collector/raw/main/install.sh)" -- -l
```

#### *(sh install.sh -l)* explained

- The gRPC framework source code is cloned by default under the "/root" folder:
- The gRPC framework is compiled and installed under the "/root/.local/{bin,include,lib,share}" folders:
- The gRPC dial-out source code is cloned/compiled under the "/opt/mdt-dialout-collector" folder:
- The building process is generating both the library and the header file required to build pmtelemetryd with gRPC dial-out support:
```SHELL
/usr/local/lib/libgrpc_collector.la
/usr/local/include/grpc_collector_bridge/grpc_collector_bridge.h
```

## Compile/Install pmtelemetryd with gRPC dial-out support enabled

```SHELL
$ sudo apt install libzmq3-dev libjansson-dev librdkafka-dev

$ cd /opt
$ sudo git clone https://github.com/pmacct/pmacct.git
$ cd /opt/pmacct
$ sudo ./autogen.sh
$ sudo ./configure --enable-debug --enable-zmq --enable-jansson --enable-kafka --enable-grpc-collector
$ sudo make -j
$ sudo make install
```