# 05 · Detection & Indicators of Compromise

Because RATs in this class **repackage and obfuscate constantly**, static file hashes age quickly. Durable detection leans on **behavioral and host indicators.** Below are categories of indicators and detection ideas, not a specific sample's hashes.

## Host / device indicators

| Indicator | Why it's suspicious |
|---|---|
| An app holds **Accessibility Service** access but isn't an assistive tool | Primary control vector for Android RATs |
| An app is registered as a **Device Administrator** without a clear reason | Used for anti-uninstall persistence |
| App **icon hidden** / app not visible in launcher but running | Stealth behavior |
| App requests a broad bundle: SMS, contacts, camera, mic, location, overlay, "install unknown apps" | Over-permissioned for its stated purpose |
| **Battery/data usage spikes** with no corresponding user activity | Background surveillance/exfiltration |
| Device **hot or active** when idle; camera/mic indicator flashes unexpectedly | Covert capture (Android 12+ shows mic/cam indicators) |
| Installed from **"unknown sources"** rather than a store | Primary delivery method |

## Network indicators

- Outbound connections from a mobile device to **non-standard TCP ports** (this family has been associated with ports such as 8080/7771, but ports are operator-configurable — treat *any* unexplained non-standard beaconing as suspect).
- **Regular beaconing** (consistent interval check-ins) to a single external host.
- Connections to hosts with no legitimate business purpose, newly registered domains, or dynamic-DNS endpoints.
- Plaintext or weakly obfuscated command/response traffic on managed networks.

> **Caution:** A specific port number is a weak IOC on its own — 8080 is also used by countless legitimate services. Correlate port + unusual host + beaconing cadence + mobile source.

## Static-analysis indicators (for lab triage)

When triaging a suspect APK in an **isolated lab** (see [07-safe-analysis-lab.md](07-safe-analysis-lab.md)), these raise the risk score:

- `AndroidManifest.xml` requesting `BIND_ACCESSIBILITY_SERVICE`, `BIND_DEVICE_ADMIN`, `SYSTEM_ALERT_WINDOW`, `RECEIVE_SMS`/`READ_SMS`, `RECORD_AUDIO`, `CAMERA`, `ACCESS_FINE_LOCATION`, `REQUEST_INSTALL_PACKAGES` together.
- A declared `AccessibilityService` with broad `canRetrieveWindowContent` / input capabilities.
- Evidence of **repackaging** (mismatched signing, injected classes, suspicious `smali`).
- Obfuscated strings, reflection-heavy loaders, or dynamically loaded `.dex`.
- Hardcoded or lightly encoded C2 host/port strings.

Tools suited to this (run only in a sandbox): **MobSF** (static+dynamic), `apktool`, `jadx`, `androguard`, and network capture via a controlled sandbox.

## Example: MobSF-style triage checklist

```
[ ] Permissions reviewed — any Accessibility / Device Admin / SMS / overlay?
[ ] Services enumerated — any AccessibilityService declared?
[ ] Receivers — BOOT_COMPLETED or event-triggered auto-start?
[ ] Certificate — self-signed? mismatched? repackaged?
[ ] Embedded URLs/IPs — unexplained external hosts/ports?
[ ] Native libs / dynamic dex loading present?
[ ] Obfuscation score / dangerous API usage flagged?
```

## Detection ideas for the enterprise

- **Mobile Threat Defense (MTD)** that flags Accessibility abuse and known RAT behaviors.
- **MDM compliance rules**: block/flag devices with sideloading enabled, unknown-source apps, or disallowed Accessibility grants.
- **Network analytics** on mobile VLAN/VPN egress for beaconing patterns.
- **UEBA** correlation: new sideloaded app + new egress destination + off-hours data transfer.

## A note on signatures vs. behavior

Signature/hash IOCs are useful for *known* samples and threat-intel sharing, but this family's constant repackaging means **behavioral detection is the durable strategy.** Prioritize the host indicators (especially Accessibility + Device Admin abuse) above any single hash.

Continue to [Mitigations](06-mitigations.md).
