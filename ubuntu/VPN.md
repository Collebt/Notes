# Shadowsokcs



```shell
# Create new chain
iptables -t nat -N SHADOWSOCKS
iptables -t mangle -N SHADOWSOCKS

# Ignore your shadowsocks server's addresses
# It's very IMPORTANT, just be careful.
iptables -t nat -A SHADOWSOCKS -d 123.123.123.123 -j RETURN

# Ignore LANs and any other addresses you'd like to bypass the proxy
# See Wikipedia and RFC5735 for full list of reserved networks.
# See ashi009/bestroutetb for a highly optimized CHN route list.
iptables -t nat -A SHADOWSOCKS -d 0.0.0.0/8 -j RETURN
iptables -t nat -A SHADOWSOCKS -d 10.0.0.0/8 -j RETURN
iptables -t nat -A SHADOWSOCKS -d 127.0.0.0/8 -j RETURN
iptables -t nat -A SHADOWSOCKS -d 169.254.0.0/16 -j RETURN
iptables -t nat -A SHADOWSOCKS -d 172.16.0.0/12 -j RETURN
iptables -t nat -A SHADOWSOCKS -d 192.168.0.0/16 -j RETURN
iptables -t nat -A SHADOWSOCKS -d 224.0.0.0/4 -j RETURN
iptables -t nat -A SHADOWSOCKS -d 240.0.0.0/4 -j RETURN

# Anything else should be redirected to shadowsocks's local port
iptables -t nat -A SHADOWSOCKS -p tcp -j REDIRECT --to-ports 12345

# Add any UDP rules
ip route add local default dev lo table 100
ip rule add fwmark 1 lookup 100
iptables -t mangle -A SHADOWSOCKS -p udp --dport 53 -j TPROXY --on-port 12345 --tproxy-mark 0x01/0x01

# Apply the rules
iptables -t nat -A PREROUTING -p tcp -j SHADOWSOCKS
iptables -t mangle -A PREROUTING -j SHADOWSOCKS

# Start the shadowsocks-redir
ss-redir -u -c /etc/config/shadowsocks.json -f /var/run/shadowsocks.pid
```



```json
{"configs" :[
{
"server" : "cu-hn-2.fsspeeder1.xyz",
"server_port" : 8008,
"password" : "kAZaFx",
"method" : "aes-256-cfb","remarks" : "",
"enable" : true
}]}

{"configs" :[
{
"server" : "cu-hn-2.fsspeeder1.xyz",
"server_port" : 8002,
"password" : "kAZaFx",
"method" : "aes-256-cfb","remarks" : "",
"enable" : true
}]}
```



启动

```shell
ss-redir -c /etc/shadowsocks/config_v1usa.json
```

