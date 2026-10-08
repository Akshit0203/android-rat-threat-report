# 03 · Capability Analysis

This section catalogs the capabilities advertised and observed in the CraxsRAT operator console, framed as **"what the threat can do to a victim"** so defenders understand the impact. The annotated figures in [`../images/`](../images/) show the operator-side control panels.

> These capabilities are common across the Android RAT class. The point is not the specific product — it is recognizing the *behaviors* so they can be detected and mitigated.

## Capability catalog

| Capability | What it means for the victim | Defensive relevance |
|---|---|---|
| **Screen capture / mirroring** | Operator sees the live screen, including anything the user types or views | Screen content = credentials, OTPs, messages all exposed |
| **Keystroke / input logging** | Everything typed is recorded | Passwords, PINs, seed phrases captured |
| **File manager** | Browse, download, and remove files on the device | Documents, photos, app data exfiltrated |
| **Application manager** | List, launch, and interact with installed apps | Can target banking/wallet apps specifically |
| **Camera access** | Activate front/rear camera remotely | Covert photography/video of the victim and surroundings |
| **Microphone capture** | Record ambient audio | Eavesdropping on conversations |
| **GPS / location tracking** | Real-time device location | Physical stalking / pattern-of-life surveillance |
| **Notification access** | Read incoming notifications | **Intercepts SMS/app-based 2FA codes** — defeats OTP MFA |
| **Contacts / SMS / call data** | Read contact lists, messages, call logs | Enables fraud, further phishing, blackmail |
| **Persistence / anti-removal** | Resists uninstallation by abusing Device Admin / Accessibility | Victim struggles to remove it without safe-mode / factory reset |
| **Stealth** | Hides its icon, mimics a legitimate app, delays malicious behavior | Harder for the user to notice infection |

## The capabilities that matter most to defenders

1. **Notification / SMS interception → MFA bypass.** This is why SMS-based OTP is weak against a compromised device. Prefer phishing-resistant MFA (passkeys/FIDO2 hardware keys) for high-value accounts.
2. **Accessibility-driven screen read + input injection.** A single granted permission unlocks most of the above. Treat Accessibility grants as a high-severity event.
3. **Anti-removal persistence.** Users should know the recovery path: boot into **Safe Mode**, revoke Device Admin, uninstall; if that fails, back up data and **factory reset**.

## Figures (operator console)

The screenshots in [`../images/`](../images/) are included as **capability evidence** for analysis. Each illustrates a control surface the operator uses against a victim:

| File | Shows | Analytical note |
|---|---|---|
| `Connection.png` | C2 connection / device check-in view | Illustrates the beaconing relationship to detect on the network |
| `Managers.png` / `Tools.png` | Operator tool menus | Inventory of capabilities to map to ATT&CK |
| `Screen Mirroring.png` | Live screen capture | Impact of screen-read abuse |
| `Camera manager.png` | Remote camera control | Covert surveillance capability |
| `File Manager.png` | Remote filesystem browsing | Data exfiltration surface |
| `Applications.png` | Installed-app enumeration | App-targeting capability |
| `Monitor.png` / `Extra.png` | Monitoring / misc features | Additional surveillance surfaces |

> If you prefer not to publish operator-console screenshots at all, you can delete `../images/` and this table — the analysis stands on its own. See the note in the root README.

Continue to the [ATT&CK Mapping](04-mitre-attack-mapping.md).
