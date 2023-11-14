# Iperf3: The ultimate speed test tool for TCP, UDP and SCTP

# 测试 TCP 吞吐

server:

```shell
iperf3 -s -i 1 -p 1314
```


client:

```shell
iperf3 -c 10.10.0.2 -i 1 -t 60 -p 1314
```


测试一分钟，输出：

```shell
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-60.01  sec   205 MBytes  28.7 Mbits/sec                  sender
[  4]   0.00-60.01  sec   205 MBytes  28.7 Mbits/sec                  receiver

iperf Done.
```

# 测试 UDP 吞吐

server:

```shell
iperf3 -s -i 1 -p 1314
```


client:

```shell
iperf3 -u -c 10.10.0.2 -b 100m -t 60 -p 1314
```