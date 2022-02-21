# coreDNS简介

# 自定义coreDNS

Corefile 配置包括以下 CoreDNS 插件：

errors：错误记录到标准输出。

health：在 http://localhost:8080/health 处提供 CoreDNS 的健康报告。

ready：在端口 8181 上提供的一个 HTTP 末端，当所有能够 表达自身就绪的插件都已就绪时，在此末端返回 200 OK。

kubernetes：CoreDNS 将基于 Kubernetes 的服务和 Pod 的 IP 答复 DNS 查询。你可以在 CoreDNS 网站阅读更多细节。 你可以使用 ttl 来定制响应的 TTL。默认值是 5 秒钟。TTL 的最小值可以是 0 秒钟， 最大值为 3600 秒。将 TTL 设置为 0 可以禁止对 DNS 记录进行缓存。

pods insecure 选项是为了与 kube-dns 向后兼容。你可以使用 pods verified 选项，该选项使得 仅在相同名称空间中存在具有匹配 IP 的 Pod 时才返回 A 记录。如果你不使用 Pod 记录，则可以使用 pods disabled 选项。

prometheus：CoreDNS 的度量指标值以 Prometheus 格式在 http://localhost:9153/metrics 上提供。
forward: 不在 Kubernetes 集群域内的任何查询都将转发到 预定义的解析器 (/etc/resolv.conf).
cache：启用前端缓存。
loop：检测到简单的转发环，如果发现死循环，则中止 CoreDNS 进程。
reload：允许自动重新加载已更改的 Corefile。 编辑 ConfigMap 配置后，请等待两分钟，以使更改生效。
loadbalance：这是一个轮转式 DNS 负载均衡器， 它在应答中随机分配 A、AAAA 和 MX 记录的顺序。
