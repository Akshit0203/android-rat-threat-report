# 02 · Attack Chain (Defender's View)

This is the lifecycle of a typical CraxsRAT-class infection, described so defenders can identify **where to intervene at each stage.** It is a model of adversary behavior, not a procedure.

```
┌─────────────┐   ┌─────────────┐   ┌──────────────┐   ┌─────────────┐   ┌──────────────┐
│ 1. Lure &   │ → │ 2. Install  │ → │ 3. Permission│ → │ 4. Command  │ → │ 5. Surveil & │
│  Delivery   │   │  (sideload) │   │   Grant      │   │  & Control  │   │  Exfiltrate  │
└─────────────┘   └─────────────┘   └──────────────┘   └─────────────┘   └──────────────┘
   phishing/         APK from          Accessibility       beacon to          data, audio,
   fake app          unknown source    + Device Admin      C2 server          camera, GPS
```

## Stage 1 — Lure & delivery
**Adversary behavior:** The malicious APK is disguised as a legitimate or desirable app (a bank app, a media player, a "system update", a cracked game) and distributed via phishing links, messaging apps, fake stores, or watering-hole sites.

**Defender intervention:**
- User awareness: never install apps from links or outside official stores.
- URL/attachment filtering; block known malware-distribution domains.
- Mobile Threat Defense (MTD) that scans sideload attempts.

## Stage 2 — Installation
**Adversary behavior:** The victim must enable "Install unknown apps" for the source and approve the install. The app often uses a minimal initial permission set to look harmless.

**Defender intervention:**
- Enterprise policy (MDM) that **disables sideloading / unknown sources** entirely.
- Google Play Protect enabled.
- Managed app catalogs so users never need to sideload.

## Stage 3 — Permission grant (the pivot point)
**Adversary behavior:** After install, the app walks the user through enabling **Accessibility Services** (and sometimes Device Administrator), often with deceptive prompts ("Enable to continue"). This is the moment control is handed over.

**Defender intervention:**
- Train users that **no normal app needs Accessibility** unless it is an assistive tool they deliberately chose.
- MDM policies restricting which apps may hold Accessibility/Device Admin.
- Periodic audits of `Settings → Accessibility` and active Device Admin apps.

## Stage 4 — Command & Control (C2)
**Adversary behavior:** The implant beacons out to an operator-controlled server to receive commands. Traffic often targets non-standard TCP ports and may be plaintext or lightly obfuscated.

**Defender intervention:**
- Network monitoring for beaconing to unusual hosts/ports from mobile subnets.
- DNS filtering and egress controls on managed networks.
- Threat-intel feeds for known C2 infrastructure.

## Stage 5 — Surveillance & exfiltration
**Adversary behavior:** With control established, the operator can capture the screen, log keystrokes, read files and messages, track GPS, and activate the microphone/camera — streaming it to the C2.

**Defender intervention:**
- This stage is already "post-compromise"; the priority is **detection and response**: isolate the device, rotate credentials, wipe/reimage.
- Anomaly detection (unexpected camera/mic usage indicators, battery/data spikes).

## Where defense is cheapest

Intervening at **Stages 1–3** (delivery, install, permission) is far cheaper and more reliable than trying to catch Stage 4–5 activity after compromise. User education plus "no sideloading" policy neutralizes the majority of this threat class.

Continue to the [Capability Analysis](03-capability-analysis.md).
