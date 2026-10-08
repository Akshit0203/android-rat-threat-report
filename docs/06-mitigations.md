# 06 · Mitigations

Defenses organized by audience. The highest-leverage controls are at the top of each list.

## For individuals / end users

1. **Only install apps from official stores** (Google Play, your device vendor's store). Keep "Install unknown apps" **disabled** for all sources.
2. **Never grant Accessibility access** unless you specifically installed an assistive tool and understand why it needs it. This is the #1 defense.
3. **Audit permissions regularly:** `Settings → Apps → [app] → Permissions`, and `Settings → Accessibility` for anything you don't recognize. Remove unknown Device Admin apps under `Settings → Security → Device admin apps`.
4. **Keep Google Play Protect on** and keep the OS updated.
5. **Use phishing-resistant MFA** (passkeys / FIDO2 hardware keys) for important accounts instead of SMS OTP, which a device-resident RAT can intercept.
6. **Be skeptical of links** promising apps, updates, or "required" installs via SMS/chat/email.

### If you suspect infection
- Disconnect from the network (airplane mode).
- Boot into **Safe Mode** (disables third-party apps), revoke the suspicious app's Device Admin, then uninstall.
- If it resists removal, **back up personal data and factory reset.**
- **Change passwords from a clean device** and review account/financial activity. Rotate anything typed on the device.

## For enterprises / IT & security teams

1. **Policy: no sideloading.** Use MDM/UEM to disable unknown sources and enforce a managed app catalog.
2. **Restrict Accessibility & Device Admin** to an allowlist via MDM; alert on new grants.
3. **Deploy Mobile Threat Defense (MTD)** integrated with conditional access, so risky devices lose access to corporate resources.
4. **Separate corporate data** with work profiles / app protection policies, limiting what a compromised personal space can reach.
5. **Network controls:** monitor mobile egress for beaconing; apply DNS filtering and threat-intel blocklists.
6. **Prefer phishing-resistant MFA** org-wide for high-value systems.
7. **Incident response runbook** for mobile: isolate, revoke tokens/sessions, wipe/reimage, investigate blast radius.
8. **User awareness training** specifically covering sideloading and Accessibility-prompt social engineering.

## For Android app developers

1. **Protect sensitive screens** with `FLAG_SECURE` to resist screen capture/mirroring.
2. **Harden against overlay attacks** (`SYSTEM_ALERT_WINDOW` abuse) on sensitive flows; detect `obscured` touch events.
3. **Use the Play Integrity API** to verify the app is unmodified and running on a genuine device/app context.
4. **Minimize and justify permissions**; follow least privilege so your app doesn't look like — or become a template for — over-permissioned malware.
5. **Certificate pinning** and server-side anomaly detection for your app's traffic.

## Control-to-stage summary

| Attack stage | Cheapest effective control |
|---|---|
| Delivery | User awareness + URL filtering |
| Install | **Disable sideloading / unknown sources** |
| Permission grant | **Deny Accessibility to non-assistive apps**; MDM allowlist |
| C2 | Network egress monitoring + DNS filtering |
| Exfiltration | Detection & response (isolate, rotate, wipe) |

Continue to [Safe Analysis Lab](07-safe-analysis-lab.md).
