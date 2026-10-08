# 01 · Overview & Threat Context

## Family at a glance

| Attribute | Detail |
|---|---|
| **Name** | CraxsRAT |
| **Type** | Android Remote Access Trojan (RAT) / commodity spyware |
| **Platform** | Android |
| **Delivery** | Trojanized / repackaged APKs, sideloaded (not from official stores) |
| **Builder** | Windows-based builder that generates the malicious APK and runs the operator console |
| **Control vector** | Abuse of Android **Accessibility Services** + requested runtime permissions |
| **Operator model** | Commercially sold "malware-as-a-service"; low skill barrier to use |
| **Threat class** | Same behavioral family as SpyNote, Hydra, Cerberus, and other Android RAT/stalkerware |

## Why Android RATs matter

Smartphones concentrate a person's most sensitive data — messages, banking, location, camera, and microphone — behind a single unlock. A RAT that lands on a phone effectively becomes a **live surveillance implant**. For enterprises, a single infected BYOD device can become a foothold into corporate mail, VPN, and MFA tokens.

Commodity RATs like CraxsRAT lower the barrier dramatically: the operator does not need to write exploits. They need only **social-engineer a user into installing a disguised app and granting Accessibility access.** That makes user awareness and device policy — not just technical controls — central to defense.

## The core abuse pattern (the one thing to remember)

Almost every Android RAT, including this one, relies on the same chain:

```
Disguised APK  →  user installs (sideload)  →  app requests Accessibility
     →  user grants it  →  attacker gains near-complete remote control
```

**Accessibility Services** exist to help users with disabilities (reading the screen aloud, automating taps). When abused, they let a malicious app *read everything on screen* and *inject input* — which is why they are the single most important permission to defend.

## Scope of this analysis

This repository focuses on the **defensive understanding** of the threat:

- **In scope:** capabilities, lifecycle, ATT&CK mapping, detection ideas, IOCs, mitigations, and how to study samples safely.
- **Out of scope (intentionally):** building, configuring, obfuscating, deploying, or operating the malware; evading antivirus; or any instruction that would help someone attack a device.

See the [Attack Chain](02-attack-chain.md) next.
