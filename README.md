# Marauder Scanner (Android)

> ### ⚖️ Legal / passive-only build — NO attack features
> This is a **scanner only**. Every transmit / attack feature of the upstream app
> has been **removed**: no deauth, no beacon spam, no BLE spam, no Karma, and no
> Evil Portal (its screen, HTML upload, and credential-capture code are all
> deleted). The app only *displays* what the board passively receives. See
> [Legal](#legal) below.

A **passive, receive-only** Android companion for an ESP32 running Marauder
firmware with the JSON serial interface. It connects to the board over USB-OTG
serial and shows live WiFi / BLE scan data, device lists, AirTag detection, GPS,
analyzers, and a raw serial console.

All **transmit / attack** features of the upstream app have been removed (no
deauth, beacon/BLE spam, Karma, or Evil Portal) so this is a scanner only.

Built and tested against a Seeed Studio **XIAO ESP32-C5** running the paired
firmware fork, on a Galaxy **A53 / Android 16**.

## What's different from upstream

Based on [0xsys/ESP32-Marauder-Mobile](https://github.com/0xsys/ESP32-Marauder-Mobile)
(Kotlin + Jetpack Compose). Changes:

- **Removed the attack surface:** deleted the WiFi Attacks and Bluetooth Attacks
  menus, the Evil Portal screen and its upload/credential logic, and the
  `OpenEvilPortal` action. The passive suite (sniffers, scanners, device lists,
  analyzers, GPS, console, flasher, themes, auto-connect) is unchanged.
- **Android 16 targeting:** `compileSdk` / `targetSdk` = 36 (edge-to-edge was
  already wired up). AGP 8.9.1, Gradle 8.11.1.
- No protocol changes — the app's `@J` JSON parser already matches the firmware.

## Build

- Android Studio with Android SDK Platform 36.
- JDK **17–21** to run Gradle (JDK 25 is rejected by Gradle 8.11.1 — point
  `JAVA_HOME` at a JDK 21 if your Studio bundles a newer JBR).
- `./gradlew :app:assembleDebug` → `app/build/outputs/apk/debug/app-debug.apk`,
  then sideload onto the phone.

## Use

Install the APK, open **Marauder**, and plug the ESP32 into the phone via a
USB-OTG adapter. Grant USB access when prompted; the app handshakes with
`jsoninfo` and you can scan and browse the live lists.

## Credits & license

Based on the Android app by [0xsys](https://github.com/0xsys), itself a
companion to [ESP32 Marauder](https://github.com/justcallmekoko/ESP32Marauder)
by justcallmekoko.

MIT licensed — see [LICENSE](LICENSE). Original copyright retained.

## Legal

Passive scanning receives broadcasts any radio can hear and is legal. This build
intentionally omits all transmit features; use it within your local laws.
