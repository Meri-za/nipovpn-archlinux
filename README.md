# NipoVPN
This is a FORKED version of [NIPOVPN](https://github.com/MortezaBashsiz/nipovpn/tree/main) by [MortezaBashsiz](https://github.com/MortezaBashsiz) for Arch Linux.

## Overview
NipoVPN is a powerful proxy tool designed to conceal your HTTP requests within fake HTTP requests. This program, written in C++, leverages the Boost library to handle networking functionalities efficiently.

## Features
  - HTTP Request Obfuscation: Hide your legitimate HTTP requests inside decoy requests to avoid detection.
  - Boost Library Integration: Utilizes Boost for robust and reliable networking operations.
  - High Performance: Optimized for speed and efficiency, ensuring minimal impact on request latency.
  - Support HTTP and SOCKS5 on agent side
  - Ability to use multiple Agents for one Server

## Makepkg
```bash
[~/]>$ git clone https://github.com/Meri-za/nipovpn-archlinux.git && cd nipovpn-archlinux
[~/nipovpn]>$ makepkg -si
```

## Services For Agent
```bash
[~/nipovpn]>$ sudo systemctl enbale --now nipovpn-agent.service
[~/nipovpn]>$ sudo systemctl start --now nipovpn-agent.service
```

## Services For Server
```bash
[~/nipovpn]>$ sudo systemctl enbale --now nipovpn-server.service
[~/nipovpn]>$ sudo systemctl start --now nipovpn-server.service
```

## Pick a shared token
`general.token` must be at least 32 bytes and identical on the agent and the
server. Do not use the sample token from the shipped config.

```bash
openssl rand -hex 16   # prints 32 hex characters
```

## TLS certificate (if `tlsEnable: true`)
The server needs a certificate and key. A self-signed pair is enough when
`tlsVerifyPeer` is `false`:

```bash
sudo openssl req -x509 -newkey rsa:2048 -nodes -days 3650 \
  -subj "/CN=example.com" \
  -keyout /etc/nipovpn/server.key -out /etc/nipovpn/server.crt
```

## Run Server
On the server, set `server.listenIp`/`server.listenPort`, then:

```bash
sudo nipovpn server /etc/nipovpn/config.yaml
```

## Run Agent
On your machine, set `agent.serverIp`/`agent.serverPort` to the server's
address and make sure `token`, `aesEnable`, `tlsEnable` and `tunnelEnable` match
the server. Then:

```bash
sudo nipovpn agent /etc/nipovpn/config.yaml
```

## Config Path
```bash
cat /etc/nipovpn/config.yaml
```

## Log Path
```bash
tail -f /var/log/nipovpn/nipovpn.log
```

## Removing
```bash
[~/]>$ sudo pacman -Rc nipovpn nipovpn-debug
```

Check out the [Configuration reference](https://github.com/MortezaBashsiz/nipovpn/blob/main/README.md?plain=1) for more details.
