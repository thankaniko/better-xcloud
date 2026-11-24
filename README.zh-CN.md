# BX Community Final — 无限期暂停开发

**Idiomas / Languages / Idiomas / 语言:** [Português (Brasil)](README.md) · [English](README.en.md) · [Español](README.es.md) · [简体中文](README.zh-CN.md)

> [!IMPORTANT]
> **项目正式声明 · 2026 年 11 月 24 日。** 最终实验版本 1.0.0。开发已无限期暂停，不计划提供后续更新、安全补丁、技术支持或未来兼容性保证。本版本并非稳定发行版。

## 1. 公开声明与原因

本独立项目旨在改善 LG 电视上的云游戏体验，包括未获得官方客户端支持的设备。项目的目标始终是技术性的：让串流指标可测量、充分利用现有硬件能力，并探索无需 root 权限的兼容方案。

我们决定无限期暂停开发，以和平方式表达对 Xbox Cloud Gaming 商业政策调整的反对。Xbox 在 [2026 年 9 月 3 日的公告](https://news.xbox.com/en-us/2026/09/03/xbox-cloud-gaming-changes/) 中宣布，对此前不受此类月度时长限制的 Game Pass 云游戏服务引入每月游戏时长额度，并提供购买额外串流时长的选项。公告将运营成本、服务可靠性及持续投资列为调整原因。实际适用条件可能因账户和市场而异。

我们反对的是订阅核心权益的缩减，尤其是对依赖云游戏的用户所造成的影响。我们理解基础设施成本以及商业模式可持续发展的需要。然而，我们认为，限制此前不受此类额度约束的权益，并对继续使用服务另行收费，会削弱可预期性、消费者信任及订阅价值。我们倡导透明的服务条款、充分的提前通知，以及对依赖该服务的用户采取合理且相称的措施。

本声明是对商业政策的批评，并非认定违法、指控未经证实的动机，或攻击员工、开发者和用户。我们不声称微软抄袭了其他服务提供商。本项目不旨在绕过游戏时长额度、付费要求或订阅资格，不制造滥用性网络流量，也不破坏服务。我们不鼓励骚扰或未经授权的访问。

最终实验软件包及其源代码继续公开，供存档、学习和技术研究。保留成果不意味着持续维护，也不意味着原有技术目标已经全部实现。没有保证恢复开发的日期或条件。本决定仅适用于本独立移植项目，不代表 Better xCloud 原作者或独立的 webOS Mega Repository 项目。

## 2. 最终软件包

[IPK](final/org.webos.community.bxfinal_1.0.0_all.ipk) · [Source ZIP](final/bx-community-final-source.zip)

| 项目 | 状态 |
| --- | --- |
| 版本 | 1.0.0 — 实验版 |
| 安装 | webOS Developer Mode；无需 root |
| 网络 | Xbox 官方网站；无需项目自建代理、NAS 或服务器 |
| 目标 | 2020 年及之后的 LG 电视；并非已认证兼容列表 |
| 验证 | 软件包结构、JavaScript 语法及模拟测试；最终版本的真机串流尚未验证 |
| 维护 | 无限期暂停 |

## 3. 技术行为

独立启动器打开 https://play.xbox.com/。用户脚本设计为仅在 Xbox 官方源站运行，排除身份验证路径。不主动收集、导出或记录凭据、Cookie、令牌、请求头或 URL；没有项目自建遥测后端。这是对实现方式的描述，并非独立安全认证。微软自身服务仍遵循其正常的数据处理方式。

| 配置 | 行为与限制 |
| --- | --- |
| Maximum（默认） | 不额外施加本地码率或帧率上限。在现代 Chromium 中优先选择浏览器声明支持的高效率编解码器；可选择 Auto 或 AVC。不保证实际协商结果或硬件加速。 |
| Native | 禁用编解码器偏好及请求修改，保留本地监控。 |
| HQ Legacy（实验） | 仅在现有会话请求包含必要字段时，采用上游 Tizen 设备配置技术。不改变浏览器版本、尺寸或编解码能力，不将数据重定向至外部。可能导致画质下降或串流失败；请切换 Native + Auto 并手动重新启动会话。不保证自动恢复。 |

通过 Xbox 原生画质选择器请求服务提供的最高分辨率。本软件不强制使用不可用的分辨率，不突破服务器码率限制，也不绕过访问资格。不保证 4K/8K、HDR、AV1、HEVC、120 FPS 或任意码率；没有自建编码器或超分辨率算法。Xbox 文档说明符合条件的场景可达到 1440p。实际表现取决于服务、屏幕、解码器和网络。

本地面板显示 RTP/HTML 视频分辨率、FPS、码率、丢包、抖动、RTT、丢帧、编解码器、平均 QP、解码时间及 QPS。QP 表示量化指标，而非对远程编码器的控制。QPS 只统计观察到的、发往串流源站的 fetch 请求，不包括 XHR、其他主机、workers 或 WebRTC 流量；不会人为增加 QPS。N/D 表示无法获取数据，并非零值。不检查外部 frame 或 worker。此前的 Full/Lite 构建未集成，仅采用上游独立的设备配置技术。

## 4. 兼容性、安装与安全

目标系统为 webOS 5.x（2020）、6.x（2021）、22、23、24、25、26 及后续版本。保守语法、API 检测及回退机制不能证明实际兼容性。最终 IPK 尚未在上述任何一代设备上完成真机验证。浏览器、身份验证、网站结构或服务政策的变化可能导致软件无法运行。

1. 使用 Developer Mode 和 webOS Dev Manager 安装 IPK。独立应用 ID 不会覆盖 Probe 0.2.0。
2. 打开启动器，选择 Xbox 原生最高可用画质并启动游戏会话。
3. 在面板中修改配置或编解码器后重新启动游戏会话。键盘 F8 可切换面板显示；重启应用可恢复界面。手柄输入仍由页面处理。
4. 如串流失败，请选择 Native + Auto 并重启，或卸载软件并使用官方客户端。如果实际登录源站不是微软官方身份验证域名，请勿输入凭据；如无法确认，请停止操作。

即使出现安全或兼容性问题，也没有后续更新计划。日常使用建议选择官方客户端。静态检查及模拟测试不能替代真机验证或安全审计。软件根据 MIT 许可证条款按现状提供。

## 5. 构建复现与完整性

解压源代码 ZIP，在其根目录执行以下命令（需要 Python 3、`ar` 和 Node.js）：

```sh
python3 build.py
node --check app/probe.js
node --check app/webOSUserScripts/userScript.js
node tests/mock.js
```

打包过程中已验证软件包结构、JavaScript 语法，以及作用范围、编解码器和回退机制的模拟测试。这不能证明真机可用性。请核对未修改的分发文件的 SHA-256：

| File | SHA-256 |
| --- | --- |
| `org.webos.community.bxfinal_1.0.0_all.ipk` | `414a24412dba77639932691c3b6f616657b912bccd612cc4b9f73c46002aac36` |
| `bx-community-final-source.zip` | `3aa1412ab473e4dc6e6308f7e57ec86ecd3963515797003e2699024777a0c2ab` |

[final/](final/) 中的 ZIP 和 IPK 为存档文件，不是稳定的 GitHub Release，也未纳入 webOS Mega Repository 主目录。本次文档修订未修改存档的二进制文件或源代码 ZIP。

## 6. 参考资料与署名

本项目独立且非官方，与微软、Xbox、LG 或原维护者无隶属关系。基于 redphx 的 Better xCloud，采用 MIT 许可证；保留原始版权声明及署名。商标归各自权利人所有。上游 README 单独保存，以免将其支持和捐赠说明与本暂停开发的移植项目混淆。

- [Xbox Wire — cloud gaming policy announcement (2026-09-03)](https://news.xbox.com/en-us/2026/09/03/xbox-cloud-gaming-changes/)
- [Xbox Wire — 1440p streaming](https://news.xbox.com/pt-br/2026/02/25/atualizacao-de-fevereiro-do-xbox-streaming-em-1440p-nos-consoles-xbox-atualizacoes-do-rog-xbox-ally-e-mais/)
- [Better xCloud](https://github.com/redphx/better-xcloud) · [Features](https://better-xcloud.github.io/features/) · [FAQ](https://better-xcloud.github.io/faq/)
- [LG webOS — Web API and web engine](https://webostv.developer.lge.com/develop/specifications/web-api-and-web-engine)
- [webOS Brew — userscripts](https://www.webosbrew.org/pages/web-development/#userscripts-in-apps)
- [W3C — WebRTC](https://www.w3.org/TR/webrtc/)
- [MIT LICENSE](LICENSE) · [Original upstream README](docs/UPSTREAM-README.md)

**最终状态：无限期暂停开发。** 不承诺恢复、修复或更新。
