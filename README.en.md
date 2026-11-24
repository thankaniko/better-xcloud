# BX Community Final — development suspended indefinitely

**Idiomas / Languages / Idiomas / 语言:** [Português (Brasil)](README.md) · [English](README.en.md) · [Español](README.es.md) · [简体中文](README.zh-CN.md)

> [!IMPORTANT]
> **Official project statement · 24 November 2026.** Final experimental version 1.0.0. Development is suspended indefinitely. No further updates, security patches, technical support or future compatibility guarantees are planned. This is not a stable release.

## 1. Public statement and rationale

This independent initiative was created to improve cloud gaming on LG televisions, including devices without official client support. Its purpose was technical: to make streaming measurable, use available hardware capabilities and investigate compatibility without root privileges.

We have deliberately suspended development as a peaceful protest against changes to Xbox Cloud Gaming's commercial policy. In its [announcement of 3 September 2026](https://news.xbox.com/en-us/2026/09/03/xbox-cloud-gaming-changes/), Xbox described the introduction of monthly playtime allowances in Game Pass subscriptions previously available without such monthly limits, and the option to purchase additional streaming time. The announcement identified operating costs, reliability and continued investment as reasons for the change. Actual conditions may vary by account and market.

Our objection concerns the reduction of a central subscription benefit, especially for people who depend on cloud gaming. We recognize infrastructure costs and the need for sustainable business models. Nonetheless, in our assessment, restricting a previously unlimited benefit and charging separately for continued access weakens predictability, consumer confidence and the value of the subscription. We advocate transparent terms, adequate advance notice and proportionate treatment of users who rely on the service.

This is a policy criticism, not a finding of illegality, an allegation of undisclosed motives, or an attack on employees, developers or users. We do not claim that Microsoft copied another provider. This project does not seek to circumvent playtime allowances, payments or subscription eligibility, generate abusive traffic, or sabotage the service. We do not encourage harassment or unauthorized access.

The source and final experimental package remain available for archival, educational and technical purposes. Preservation does not imply ongoing maintenance or completion of the original engineering objectives. There is no date or condition guaranteeing resumption. This statement applies only to this independent port, not the upstream Better xCloud project or the separate webOS Mega Repository.

## 2. Final package

[IPK](final/org.webos.community.bxfinal_1.0.0_all.ipk) · [Source ZIP](final/bx-community-final-source.zip)

| Item | Status |
| --- | --- |
| Version | 1.0.0 — experimental |
| Installation | webOS Developer Mode; no root |
| Network | Official Xbox website; no project proxy, NAS or dedicated server |
| Target | LG TVs from 2020 onward; not a certified compatibility list |
| Validation | Package structure, JavaScript syntax and simulated tests; final hardware streaming unverified |
| Maintenance | Suspended indefinitely |

## 3. Technical behavior

The standalone launcher opens https://play.xbox.com/. Its userscript is designed to run only on official Xbox origins, excluding authentication routes. It does not intentionally collect, export or log credentials, cookies, tokens, request headers or URLs. It has no project telemetry backend. This is a description of the implementation, not an independent security certification; Microsoft's own services retain their normal data practices.

| Profile | Behavior and limitations |
| --- | --- |
| Maximum (default) | No additional local bitrate or FPS cap. Prefers efficient codecs on modern Chromium when advertised by the browser; Auto or AVC may be selected. Negotiation and hardware acceleration are not guaranteed. |
| Native | Disables codec preferences and request modifications while retaining local monitoring. |
| HQ Legacy (experimental) | Adapts the upstream Tizen device-profile technique only when the existing session request has the required fields. Does not change browser version, dimensions or codec capability. No external redirection. May degrade or break streaming; switch to Native + Auto and restart the session manually. No automatic recovery is promised. |

Use the Xbox quality selector to request the highest offered resolution. There is no mechanism to force unavailable resolutions, override server bitrate limits or bypass entitlements. 4K/8K, HDR, AV1, HEVC, 120 FPS and arbitrary bitrates are not guaranteed; there is no custom encoder or upscaler. Xbox documents up to 1440p in eligible scenarios. Actual delivery depends on service, panel, decoder and network.

Local measurements include RTP/HTML video resolution, FPS, bitrate, packet loss, jitter, RTT, dropped frames, codec, average QP, decode time and QPS. QP measures quantization, not remote encoder control. QPS counts observed fetch requests to the streaming origin only; it excludes XHR, other hosts, workers and WebRTC traffic. The app does not increase QPS artificially. N/D means unavailable, not zero. External frames and workers are not inspected. Earlier Full/Lite bundles are not included; only the isolated upstream profile technique is adapted.

## 4. Compatibility, installation and security

The target is webOS 5.x (2020), 6.x (2021), 22, 23, 24, 25, 26 and later. Conservative syntax, API detection and fallbacks do not establish compatibility. The final IPK has not been physically validated on any of these generations. Changes in browser engines, authentication, site structure and service policies may prevent operation.

1. Use Developer Mode and webOS Dev Manager to install the IPK. Its independent ID preserves Probe 0.2.0.
2. Open the launcher, choose the highest native Xbox quality option and start a session.
3. Change profile or codec via the panel and restart the game session. F8 on a keyboard toggles the panel; restarting the app restores the interface. Controller input remains with the page.
4. If streaming fails, select Native + Auto and restart, or uninstall and use the official client. Do not enter credentials unless the actual sign-in origin is an official Microsoft authentication domain; if uncertain, stop.

No updates are planned even for security or compatibility issues. The official client is recommended for regular use. Static checks and mocked tests do not replace empirical testing or security review. The MIT license supplies the software as is, subject to its terms.

## 5. Reproduction and integrity

Extract the source ZIP. Run the following from its root (Python 3, `ar` and Node.js required):

```sh
python3 build.py
node --check app/probe.js
node --check app/webOSUserScripts/userScript.js
node tests/mock.js
```

The package structure, JavaScript syntax and simulated scope, codec and fallback checks were validated during packaging. This does not establish real-device operation. Verify the SHA-256 of the unchanged distributed files:

| File | SHA-256 |
| --- | --- |
| `org.webos.community.bxfinal_1.0.0_all.ipk` | `414a24412dba77639932691c3b6f616657b912bccd612cc4b9f73c46002aac36` |
| `bx-community-final-source.zip` | `3aa1412ab473e4dc6e6308f7e57ec86ecd3963515797003e2699024777a0c2ab` |

The ZIP and IPK in [final/](final/) are archival artifacts, not a stable GitHub Release or a package in the main webOS Mega Repository catalog. This documentation revision does not modify the archived binary or source ZIP.

## 6. References and attribution

Independent, unofficial project; no affiliation with Microsoft, Xbox, LG or the original maintainers. Based on Better xCloud by redphx under MIT; original notices and credits are preserved. Trademarks belong to their respective owners. The upstream README is kept separately to avoid confusing upstream support and donation instructions with this suspended port.

- [Xbox Wire — cloud gaming policy announcement (2026-09-03)](https://news.xbox.com/en-us/2026/09/03/xbox-cloud-gaming-changes/)
- [Xbox Wire — 1440p streaming](https://news.xbox.com/pt-br/2026/02/25/atualizacao-de-fevereiro-do-xbox-streaming-em-1440p-nos-consoles-xbox-atualizacoes-do-rog-xbox-ally-e-mais/)
- [Better xCloud](https://github.com/redphx/better-xcloud) · [Features](https://better-xcloud.github.io/features/) · [FAQ](https://better-xcloud.github.io/faq/)
- [LG webOS — Web API and web engine](https://webostv.developer.lge.com/develop/specifications/web-api-and-web-engine)
- [webOS Brew — userscripts](https://www.webosbrew.org/pages/web-development/#userscripts-in-apps)
- [W3C — WebRTC](https://www.w3.org/TR/webrtc/)
- [MIT LICENSE](LICENSE) · [Original upstream README](docs/UPSTREAM-README.md)

**Final status: development suspended indefinitely.** No commitment to resume, repair or update.
