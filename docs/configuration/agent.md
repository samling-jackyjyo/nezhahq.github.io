---
outline: deep
---

# Agent 配置

Agent 配置文件格式为 YAML。

在管理后台中，可以对 Agent 的配置进行修改并直接应用；也可以通过 API 批量下发配置项，详见 [API 文档](/developer/api.html)。

---

## 选项

- ##### **`client_secret`**

  - 用于与 Dashboard 进行安全通信的客户端密钥。
  - 此参数必须与 Dashboard 中的配置相同，否则 Agent 无法正常与服务器通信。

- ##### **`debug`**

  - 当为 `true` 时启用日志。

- ##### **`disable_auto_update`**

  - 当为 `true` 时禁用 Agent 的自动更新功能，增强系统稳定性和安全性。

- ##### **`disable_command_execute`**

  - 当为 `true` 时 Agent 不再接受面板下达的 **命令执行**、**在线终端** 和 **文件列表** 任务。

- ##### **`disable_force_update`**

  - 当为 `true` 时禁用强制更新功能，仅允许手动更新。

- ##### **`disable_nat`**

  - 当为 `true` 时 Agent 不再接受面板下达的 **内网穿透** 任务。

- ##### **`disable_send_query`**

  - 当为 `true` 时 Agent 不再接受面板下达的 `TCP Ping`、`ICMP Ping` 和 `HTTP GET` 任务。

- ##### **`gpu`**

  - 当为 `true` 时启用 GPU 监控。
  - 注意：启用 GPU 监控可能需要安装额外依赖，详细信息参考：[启用 GPU 监控](/guide/q9.html)。

- ##### **`insecure_tls`**

  - 当为 `true` 时禁用证书检查，适用于使用自签名证书的场景。

- ##### **`ip_report_period`**

  - 设置本地 IP 更新间隔时间（秒）。默认值为 `1800` 秒（30 分钟）。
  - 最低有效值为 30 秒。

- ##### **`report_delay`**

  - 设置系统信息上报的时间间隔（秒）。默认值为 `3` 秒（有效范围：1-4 秒）。

- ##### **`server`**

  - 与 Dashboard 通信的域名或 IP 地址，需包括端口号。

- ##### **`skip_connection_count`**

  - 当为 `true` 时禁用网络连接数的监控，适用于高连接数或资源受限的环境。

- ##### **`skip_procs_count`**

  - 当为 `true` 时禁用进程数的监控，以降低资源占用。

- ##### **`temperature`**

  - 当为 `true` 时启用硬件温度监控（仅支持部分硬件，部分 VPS 可能无法获取温度信息）。

- ##### **`tls`**

  - 当为 `true` 时启用 Agent 与 Dashboard 间的通信 SSL/TLS 加密。
  - 如果 Agent 使用 Nginx 反向代理且启用了 SSL/TLS 配置，请开启此选项。

- ##### **`hard_drive_partition_allowlist`**

  - 一个字符串数组，用于指定需要监控的硬盘分区列表。
  - 若指定此参数，将仅对列出的分区进行监控。

- ##### **`nic_allowlist`**

  - 一个 `map[string]bool` 类型的允许列表，用于指定需要监控的网卡。
  - 键为网卡名称，值为 `true` 表示允许监控，`false` 表示不监控。
  - 若不指定或为空，则默认监控所有可用网卡。

- ##### **`use_gitee_to_upgrade`**

  - 当为 `true` 时使用 Gitee 仓库作为自动更新源，对中国大陆服务器更为友好。

- ##### **`use_ipv6_country_code`**

  - 当为 `true` 时强制使用 IPv6 地址查询国家代码（默认使用 IPv4）。

- ##### **`uuid`**

  - 当前 Agent 的唯一标识参数，用于 Dashboard 识别数据来源。
  - 若需替换 Dashboard 中已存在的 Agent，可以手动设置此参数。

- ##### **`dns`**

  - 一个字符串数组，用于设置自定义 DNS 服务器列表。
  - 指定后，Agent 将优先使用此列表中的 DNS 服务器解析域名。

- ##### **`custom_ip_api`**

  - 一个字符串数组，用于指定自定义 IP 查询 API 列表。
  - Agent 将通过这些 API 获取服务器的公网 IP 信息。

- ##### **`self_update_period`**
  - 手动设置更新间隔（分钟）。
  - 默认为 30 到 90 之间的随机值。

---

## 应用

在修改配置文件中的参数后，需要重新启动 Agent 服务以使更改生效。可以使用 Agent 的内置服务管理功能或者手动重启。

### 使用内置服务管理

可以直接输入以下命令重启默认 Agent 服务：

```shell
./agent service restart
```

对于多个 Agent 服务的情况，可以指定对应的配置文件：

```shell
./agent service -c ./config-6sc1f.yml restart
```

### 手动管理

1. **重新启动服务**  
   运行以下命令重新启动默认的第一个 Agent 服务：

   ```shell
   sudo systemctl restart nezha-agent.service
   ```

2. **多 Agent 服务的情况**  
   如果同一服务器上运行了多个 Agent 服务，请先列出所有 Agent 服务的名称：
   ```shell
   sudo systemctl list-units --type=service | grep nezha-agent
   ```
   然后分别使用以下命令重新启动对应的 Agent 服务：
   ```shell
   sudo systemctl restart <service-name>
   ```
   将 `<service-name>` 替换为实际的服务名称，例如 `nezha-agent@2.service`。
