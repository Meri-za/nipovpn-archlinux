# NipoVPN
This is a FORKED version of NIPOVPN for ARCHLINUX

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

## Run
```bash
sudo nipovpn agent /etc/nipovpn/config.yaml
sudo nipovpn server /etc/nipovpn/config.yaml
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
