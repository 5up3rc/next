# next
[![build](https://travis-ci.org/chzyer/next.svg)](https://travis-ci.org/chzyer/next)

### install

```shell
$ go get github.com/chzyer/next
```

### server

```shell
$ next sysenv -iface eth0 # enable ipforward and NAT, only work for linux
$ next genkey
617e819c1551a6be8e31b76ed5cb8157
$ next server -key 617e819c1551a6be8e31b76ed5cb8157
... running...
```

add a user

```shell
$ next shell
Next Server CLI
 -> user add <userName>
password:
```

### client

```shell
$ next client -key 617e819c1551a6be8e31b76ed5cb8157 -username <userName> -password <password> <serverHost>
```

### test

```shell
ping 10.8.0.1
PING 10.8.0.1 (10.8.0.1) 56(84) bytes of data.
64 bytes from 10.8.0.1: icmp_seq=1 ttl=64 time=1.07 ms
64 bytes from 10.8.0.1: icmp_seq=2 ttl=64 time=0.971 ms
64 bytes from 10.8.0.1: icmp_seq=3 ttl=64 time=1.41 ms
64 bytes from 10.8.0.1: icmp_seq=4 ttl=64 time=1.47 ms
```

### route table
```shell
$ next shell
Next Client CLI
 -> route add 8.8.8.8/32 'google dns'
route item '8.8.8.8/32' added
 -> route show
Item:
	8.8.8.8/32	google dns
 -> ^D

$ netstat -nr | grep 8.8.8.8
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
8.8.8.8         0.0.0.0         255.255.255.255 UH        0 0          0 utun0
```

### show speed
```shell
$ watch -n 1 next shell dchan speed

Every 1.0s: next shell dchan speed

upload:   66B/s
download: 84B/s
```

### show data channels
```shell
$ watch -n 1 next shell dchan list
[1.1.1.1:62019 -> 2.2.2.2:36152]: RTT: 767ms 767ms 516ms, LC: 0, LT: 2m13s
[1.1.1.1:61992 -> 2.2.2.2:47453]: RTT: 639ms 639ms 390ms, LC: 0, LT: 2m37s [*]
[1.1.1.1:61920 -> 2.2.2.2:34667]: RTT: 780ms 780ms 336ms, LC: 1s, LT: 4m0s [*]
[1.1.1.1:61917 -> 2.2.2.2:50859]: RTT: 786ms 786ms 395ms, LC: 0, LT: 4m1s [*]

# RTT: round trip time, (15min, 5min, 1min)
# LC: last commit time
# LT: life time
# [*]: data channels which is usable
```

