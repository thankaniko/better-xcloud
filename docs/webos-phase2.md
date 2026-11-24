# Phase 2 — bundle inspection and device probe

The user supplied the smoke-build artifacts for Lite and Full. Both passed Node.js 22 syntax checks (not a browser runtime test).

| Artifact | Bytes | SHA-256 |
|---|---:|---|
| better-xcloud.webos.lite.user.js | 345790 | 20ea6b2cd188c704c47825215f5feaed932f69390a582a47ad0d3ebae1039c7f |
| better-xcloud.webos.user.js | 473819 | c417da85e173ae631928b9b3260a828a6c8b5b8f817fdf51d21931a7941677ad |

Both generated userscripts have legacy www.xbox.com play matching rules, no explicit play.xbox.com literal, and use optional chaining, nullish coalescing, static class fields, replaceAll and structuredClone. A transpilation pass alone is not sufficient to guarantee compatibility with Chromium 68/79.

## Device experiment 0.1.0

A standalone local diagnostic IPK, io.github.thankaniko.bxprobe_0.1.0_all.ipk, was supplied separately with its source ZIP in the conversation. SHA-256: a70795e4d5543fac144d79e265196f20860a039ae302a66fb3cd81f4e6197a76. Its archive structure and JavaScript syntax were checked locally; installation and runtime remain untested. This is NOT a Better xCloud streaming client and is not published in the production Mega Repository.

It uses the community-documented webOSUserScripts/userScript.js mechanism:
https://www.webosbrew.org/pages/web-development/#userscripts-in-apps

Test procedure:
1. Install through Developer Mode using webOS Dev Manager.
2. Capture the local capability report (Chromium, WebRTC, gamepad, codec declaration, WebGL2, syntax and runtime API probes).
3. Open the previous Xbox play URL and then the new play.xbox.com URL. Check for the green BX PROBE marker and record the actual hostname; close and reopen to return to the local page. Do not sign in for this experiment.
4. Record results by model and firmware without personal identifiers or credentials.

The probe does not include the upstream Lite/Full script, credential handling, proxy, telemetry, or game streaming changes. Next gates: confirm injection behavior on real hardware, review upstream host migration and authentication boundaries, then build an origin-scoped experimental streaming wrapper.
