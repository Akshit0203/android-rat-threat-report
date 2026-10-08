# 07 · Safe Analysis Lab (Responsible Study)

If you want to study Android RAT samples **hands-on**, do it in a way that cannot harm anyone. This page describes the *principles and isolation* of a responsible malware-analysis lab. It intentionally does **not** explain how to build, configure, or deploy any RAT or payload.

> **Golden rule:** A sample under analysis must never be able to reach a real person, device, account, or network. If you cannot guarantee isolation, do not run it.

## Non-negotiable safety principles

1. **Isolation first.** Analyze only inside a disposable VM or emulator that is network-isolated from your real devices and the internet (host-only networking, or a fully air-gapped setup).
2. **No real data, no real accounts.** Never sign into personal accounts, insert a real SIM, or use real credentials inside the analysis environment.
3. **No live victims, ever.** Never install a sample on a device you don't own, and never on any device belonging to another person — with or without a sample.
4. **Snapshots & disposability.** Take a clean snapshot before analysis and revert after. Treat the environment as burnable.
5. **Contain C2.** If you must observe network behavior, do it against a **simulated** service in a closed network (e.g., a sandboxing framework's fake-internet / `INetSim`-style responder) — never against a live operator server, and never operate one yourself.
6. **Legal & ethical authorization.** Only analyze samples you are lawfully permitted to possess and study. Respect your jurisdiction's laws and your organization's policy.

## Recommended, legal ways to practice

You can build real skills **without touching live malware** at all:

- **MobSF** against intentionally vulnerable / benign test apps to learn static & dynamic analysis workflow.
- **Android emulator** (AVD) snapshots for safe, resettable experimentation.
- Decompilation practice with **`jadx`** and **`apktool`** on open-source APKs.
- Curated, consent-based training material:
  - [OWASP Mobile Security Testing Guide (MSTG)](https://owasp.org/www-project-mobile-app-security/)
  - [OWASP MASVS](https://mas.owasp.org/)
  - [MITRE ATT&CK for Mobile](https://attack.mitre.org/matrices/mobile/)
  - Android's official [security documentation](https://source.android.com/docs/security).
- Capture-the-Flag (CTF) mobile challenges and sanctioned platforms where targets are provided for you.

## Toolbox (analysis, not attack)

| Tool | Use |
|---|---|
| **MobSF** | Automated static + dynamic analysis of APKs |
| **jadx / apktool** | Decompile & inspect app code and manifest |
| **androguard** | Programmatic APK analysis |
| **Android Emulator (AVD)** | Isolated, snapshot-able test device |
| **Wireshark + simulated internet** | Observe network behavior in a closed net |

## What this lab is *not* for

- Not for generating, modifying, or distributing malware.
- Not for testing against anyone's real device or account.
- Not for operating command-and-control infrastructure.

Studying how malware works so you can defend against it is legitimate and valuable. Doing it safely and lawfully is what separates a security professional from an offender. Keep it isolated, keep it consensual, keep it legal.

Back to the [README](../README.md).
