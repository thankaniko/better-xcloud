# Better xCloud community port — LG webOS 2020+

Unofficial research branch based on Better xCloud by redphx (MIT). Preserve LICENSE and upstream attribution. Not affiliated with Microsoft, Xbox, LG, or the upstream maintainer. No production IPK exists yet.

## Compatibility targets

| Generation | webOS TV | Chromium | Status |
|---|---|---|---|
| 2020 | 5.x | 68 | Experimental target, not tested |
| 2021 | 6.x | 79 | Experimental target, not tested |
| 2022 | 22 | 87 | Target, not tested |
| 2023 | 23 | 94 | Target, not tested |
| 2024 | 24 | 108 | Target, not tested |
| 2025 | 25 | 120 | Target, not tested |
| 2026 | 26 | 132 | Target, not tested |

LG engine reference: https://webostv.developer.lge.com/develop/specifications/web-api-and-web-engine
Upstream webOS baseline: https://better-xcloud.github.io/lg-webos/ (webOS 22+).
Upstream release status: https://github.com/redphx/better-xcloud/releases

## Build smoke test

Install dependencies with Bun and run:

    bun run build.ts --version 0.1.0-dev --target webos --variant lite
    bun run build.ts --version 0.1.0-dev --target webos --variant full

This produces JavaScript bundles, not installable IPKs. The current upstream baseline is Chrome >=80; lowering a transpilation target alone does not provide missing browser APIs or codecs.

## Release gates

1. Confirm an active, supported Xbox website and upstream source revision.
2. Inspect the existing TV wrapper, its injection model, dependencies, origin/cookie rules, and license; do not inject into authentication pages or collect tokens.
3. Probe browser capabilities (WebRTC, codec negotiation, secure contexts, gamepad, WebGL, JavaScript APIs). Introduce tested compatibility changes for Chromium 68/79 only where safe. Never misrepresent hardware capability.
4. Package an independently branded application with a unique ID, no root, no NAS, no credential proxy, no third-party account endpoints. Keep normal Microsoft login.
5. Verify build and IPK metadata, hashes, installation through Developer Mode, login, actual streaming, controllers, audio, recovery, latency, and session persistence on representative TVs.
6. Record results per model/firmware. Treat untested generations as targets, not supported. Publish experimental packages separately; promote to the Mega Repository only after review.

Resolution, refresh rate and feature availability depend on the service, device decoder and network. No 4K/120 FPS promise.

Do not publish credentials, debug tokens, cookies, or personal device identifiers in issues or CI logs.
