# 04 · MITRE ATT&CK (Mobile) Mapping

Mapping observed CraxsRAT-class behavior to the [MITRE ATT&CK for Mobile](https://attack.mitre.org/matrices/mobile/) matrix gives defenders a shared vocabulary and ties each behavior to published detection and mitigation guidance.

> Technique IDs reference the **Mobile** matrix. Always confirm against the current ATT&CK release, as IDs evolve.

## Mapping table

| Tactic | Technique (ID) | How it appears in this family |
|---|---|---|
| **Initial Access** | Deliver Malicious App via Other Means (T1476 / current equivalent) | Sideloaded trojanized APK from phishing or fake stores |
| **Execution** | Native/Command Execution (T1623) | Remote command handling from C2 |
| **Persistence** | Event Triggered Execution (T1624) | Auto-start on boot / on specific events |
| **Persistence / Defense Evasion** | Abuse Elevation Control Mechanism: Device Administrator Permissions (T1626.001) | Device Admin abused to resist uninstallation |
| **Defense Evasion** | Hide Artifacts: Suppress App Icon (T1628.002) | Icon hidden after install to avoid notice |
| **Defense Evasion** | Masquerading / Match Legitimate Name (T1655) | APK mimics a legitimate app's name, icon, UI |
| **Defense Evasion** | Impair Defenses (T1629) | Attempts to evade AV / resist removal |
| **Defense Evasion** | Obfuscated Files or Information (T1406) | Repacking/obfuscation to defeat signatures |
| **Collection / Control** | Input Injection (T1516) | Accessibility used to inject taps/actions |
| **Collection** | Input Capture: Keylogging (T1417.001) | Logs typed input |
| **Collection** | Access Notifications (T1517) | Reads notifications → intercepts OTP/2FA |
| **Collection** | Screen Capture (T1513) | Live screen mirroring |
| **Collection** | Video Capture (T1512) | Remote camera activation |
| **Collection** | Audio Capture (T1429) | Microphone recording |
| **Collection** | Location Tracking (T1430) | GPS surveillance |
| **Collection** | Protected User Data: Contacts (T1636.003) / SMS (T1636.004) | Reads contacts, SMS, call logs |
| **Collection** | Stored Application Data (T1409) | Accesses other apps' stored data |
| **Command & Control** | Application Layer Protocol (T1437) | C2 over TCP on non-standard ports |
| **Command & Control** | Encrypted/obfuscated channel (T1521 where applicable) | Channel obfuscation varies by build |
| **Exfiltration** | Exfiltration Over C2 Channel (T1646) | Captured data streamed to operator server |

## The pivot technique: Abuse of Accessibility

The single technique that unlocks most of this matrix is **abuse of Accessibility Services** (enabling Input Injection T1516, Screen Capture T1513, and Access Notifications T1517 in combination). If you can only monitor one thing on Android, monitor **which apps hold Accessibility access.**

## Using this mapping

- **Detection engineering:** For each technique, consult the ATT&CK page's "Detection" section and build corresponding telemetry (permission audits, network analytics, MTD signals).
- **Coverage assessment:** Check your mobile defenses against this column to find gaps (e.g., "Do we detect notification-access abuse that defeats SMS OTP?").
- **Tabletop exercises:** Walk responders through the chain in [02-attack-chain.md](02-attack-chain.md) using these technique IDs.

Continue to [Detection & IOCs](05-detection-and-iocs.md).
