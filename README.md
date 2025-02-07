# 通过CF让多个vmess负载均衡速度提升教程

![OIP-C.jpeg](https://img.877774.xyz/api/cfile/AgACAgUAAyEGAASMeqieAAOGZ4ZopT4jhQFoqA4Hr8B0Axb5M3IAAvvCMRsQAzBUzz0HDESTe34BAAMCAAN4AAM2BA)

## 说明：
本项目并非我创作，GitHub fork别人的项目的，教程我给扩充并详细讲解了一下。。。

仅供测试！！！仅供测试！！！仅供测试！！！
（秋名山修改使用说明更易懂完整，并非我原创）

转载请注明出处！

# Cloudflare Workers 负载均衡器

该项目通过 Cloudflare Workers 实现简单的服务器负载均衡，采用轮询算法分配流量到不同的服务器节点。

多个不同服务器建的vmess才能看出效果！不要只用一个vmess，无意义！

# 使用说明

使用 Workers/Pages 连接 Github 的方法部署均可；绑定自定义域后，使用这个自定义域代替伪装域名和SNI，节点的uuid需要相同。节点就是你随便打开一个你原来的节点，修改sni和伪装域名为你workers/pages的自定义域名，然后即可使用。

（点击下载[_worker.js](https://github.com/qmsdh/Serv00-LoadBalance/blob/main/_worker.js)）

## 功能

- **负载均衡**：基于轮询方式来选择服务器，不依赖 IP 哈希。
- **并行模式**：并行模式会同时向多个服务器发送请求，返回第一个成功的响应。通过向所有服务器并发发送请求，尽早返回第一个可用的结果，避免因单个服务器延迟或故障影响使用体验。

## 配置

在cloudflare workers/pages 后台添加的环境变量。

1. **环境变量**：

   - SERVERS：必填，域名列表（Argox隧道域名），每行一个地址。例如：
     ```
     s4argo.google.com
     s5argo.google.com
     s6argo.google.com
     ```
   - MODE：必填，模式选择，当MODE 为 1 时，使用轮询模式。当MODE为 2 时，使用并行模式。（填“1”或“2”）


## 使用

将此 Workers 部署到你的 Cloudflare 账户中，并将你的域名或子域名配置为使用该 Workers 脚本。所有到达 Workers 的请求将通过负载均衡器进行处理和转发。

## 许可

本项目采用 [MIT 许可](LICENSE)，你可以自由使用、修改和分发。
