## ping

[![GoDoc](https://godoc.org/github.com/glinton/ping?status.svg)](https://godoc.org/github.com/glinton/ping)

Simple (ICMP) library patterned after net/http.


### Notes Regarding ICMP Socket Permissions

System installed `ping` binaries generally have `setuid` attributes set, thus allowing them to utilize privileged ICMP sockets. This should work for applications built with this library as well, but a better approach would be to give the application the capability to create privileged ICMP sockets. To do so, run the following as the `root` user (not applicable to Windows).

```
setcap cap_net_raw=eip /path/to/your/application
```

Since this library can utilize unprivileged raw sockets on Linux and Darwin (`udp4` or `udp6` as the network). On Linux, the system group of the user running the application must be allowed to create unprivileged ICMP sockets. [See man pages icmp(7) for `ping_group_range`](http://man7.org/linux/man-pages/man7/icmp.7.html).

To allow a range of groups access to create unprivileged icmp sockets on linux (ipv4 or ipv6), run:

```
sudo sysctl -w net.ipv4.ping_group_range="GROUPID_START GROUPID_END"
```

If you plan to run your application as `root`, the aforementioned commmand is not necessary.

On Windows, running a terminal as admin should not be necessary.


### Known Issues

There is currently no support for TTL on windows, track progress at https://github.com/golang/go/issues/7175 and https://github.com/golang/go/issues/7174

Report any other issues you may find [here](https://github.com/glinton/ping/issues/new)
