# Undercover App Cloner

<p align="center">
  <img src="assets/logo.png" width="176" alt="Undercover App Cloner logo">
</p>

Undercover App Cloner creates locally signed Android app copies with separate package names and storage. Choose an installed app or an APK, configure the copy, review its settings and save the resulting APK to your library.

Developed by **Sharodshahi Al-Amin**, owner of **Undercover IT Firm**.

This repository distributes the Android APK, release documentation and branding assets. Application source code, keystores, signing passwords and private keys are not published here.

## Download and install

[Download Undercover App Cloner v0.6.0](https://github.com/savaskarofficial/Undercover-App-Cloner/releases/download/v0.6.0/Undercover-App-Cloner-v0.6.0.apk)

| Release | Details |
| --- | --- |
| Version | 0.6.0, version code 6 |
| Release status | Release |
| APK | `Undercover-App-Cloner-v0.6.0.apk` |
| Size | 5,533,426 bytes (5.28 MiB) |
| Minimum Android | Android 8.0, API 26 |
| Manager signing identity | UITF |

**APK SHA-256**

```text
5a412feca8f71ba02f184667632581d2056d4838524a3577578da9ebdeb4cad5
```

**UITF certificate SHA-256**

```text
bca52ad2acd8031cdd0279c21a609e91d718eb8a88a6de59018b0f31484999e9
```

1. Open the APK on an Android device running Android 8.0 or newer.
2. If Android asks, allow installation from the app that opened the file, then confirm installation.
3. Open Undercover App Cloner and choose **Installed apps** or **Import APK**.
4. Set the clone's name, package suffix, icon and optional batch count in **Identity**.
5. Configure **Options**, check **Review**, then select **Build clone**.
6. Use **Library** to install, open, share or export the saved clone.

Android controls the installer, unknown-source permission and the final installation decision. Device policy, package conflicts, signatures and unsupported APKs can prevent installation. The manager reports unavailable settings or permission-service failures instead of leaving a pending installation request.

### Updating the UITF-signed 0.5.0 release

Version 0.6.0 uses the same UITF signing certificate and package as the published 0.5.0 APK. Install it over that version to keep the manager's saved data and local clone-signing key. Uninstalling 0.5.0 is not required for this update.

### Moving from a development-signed manager

Version 0.6.0 is signed strictly with the UITF certificate. It cannot update an older development-signed manager in place. Android requires the old manager to be uninstalled before this differently signed APK can be installed.

**Uninstalling the old manager or clearing its storage removes its local AndroidKeyStore clone-signing key.** APK exports, profiles and app-data backups do not preserve that private key. Without it, the new manager cannot update existing clones signed by the old key. Export anything you need before changing installations; a fresh clone/package may be required, and account or database migration is not guaranteed.

## Interface and workflow

The manager uses four setup steps: **App**, **Identity**, **Options** and **Review**. Searchable categories group the available settings. **Library** stores finished APKs, **Data** groups clone-owned storage tools, and **Profiles** saves reusable configurations.

Use a different suffix for a separate clone. Reusing an existing clone package with the same signing identity permits an Android update that retains that clone's data. Batch names can contain `{n}`; up to 20 copies are validated before sequential processing begins. Completed builds remain available if a later batch is cancelled.

Profiles save settings, not live app sessions. Known fields are type checked; malformed values, fractional integers, overflow and non-finite coordinates are rejected. Unknown fields are ignored for compatibility.

## Finding the new controls

| Control | Location | How to use it |
| --- | --- | --- |
| Live icon preview | **Identity > Icon adjustments** | Compare **Original** and **Clone** while changing hue, inversion, flips and number badging. Preview and exported icon use the same renderer. Launcher masking can change the installed appearance. |
| Text replacement | **Options > Display** | Set **Find text** to `Test` and **Replace with** to `Testuuu`. Both fields stay visible, with a live example underneath. Matching is literal and case sensitive. A blank replacement removes matching text. |
| Color selection | **Options > Display** and **Notifications** | Open the status bar, navigation bar, toolbar or notification accent color control. Choose a preset, use RGB and opacity sliders or enter `#RRGGBB` / `#AARRGGBB`. **Apply** saves the selection, **Cancel** discards the draft and **Original** restores the source color. |
| Manager light or dark mode | **Help > App appearance** | Choose **System**, **Light** or **Dark**. This preference is saved for Undercover App Cloner and is separate from a clone's **Force dark mode** option. |
| Ads and trackers | **Options > Ads and tracking** | Enable the known ad-host and tracker lists, or enter custom domains before building. See the scope below. |

Text replacement applies to supported standard Android text views. Editable text, password fields, Compose text, custom canvases and other rendering systems are outside this control. The example shows how the two strings relate; it is not a live inspector of the source app's screen.

Changes to clone options take effect in newly built APKs. Rebuild and install the clone to apply them to a previously generated copy. Updating the manager alone does not rewrite an installed clone.

## Ads and tracking

**Options > Ads and tracking** provides separate controls for known ad hosts, known tracker hosts and a custom domain list. The built-in lists are included offline and contain **14 ad domains** and **11 tracker domains**. A custom list accepts up to **256 domains**, one per line.

Filtering applies to selected Java URL/connection and socket paths and supported top-level WebView loads inside the modified app. A matching request is blocked rather than routed through a hosted service. This feature does not create a device-wide VPN or install a system-wide DNS filter.

Native networking, automatic redirects, WebView subresources and unsupported clients can use other paths. Cached ads and ads served from an app's own content domains may still appear. Blocking a shared domain can also stop sign-in, images or other app content. These controls reduce matching traffic within the supported paths; they do not guarantee an ad-free app.

## Notification controls

Enable **Controls notification** before building, install the generated APK and open the clone once. Android notification permission and channel settings apply. Existing clones must be rebuilt to receive runtime changes.

- **New identity** generates supported identifiers and a device profile, saves them in the clone and restarts it. Location and time-zone changes require their separate randomization options. The package, signing key, public IP, files and account sessions stay the same.
- **Clear data** asks Android to reset this clone's own storage. Confirmation is on by default. **One-tap reset** is an explicit opt-in; a configured app lock still applies.
- **Startup data** embedded in the APK can be applied again after a reset. Clearing Android storage does not remove a preset contained in the installed APK.

Identity settings affect selected app-visible calls and fields. They do not guarantee that a server forgets an account or that every fingerprinting method returns the new values.

## Clone data tools

The Data tab and in-clone tools provide storage usage, backup, restore, file import/export, ZIP merge, cache clearing and own-data reset. Manager changes require **Allow manager data access** in the installed clone and the protected bridge. They cannot read or reset the original app's separate sandbox.

Backups cover approved clone files, preferences and databases. Optional password encryption uses authenticated AES-GCM with PBKDF2 key derivation. Backup passwords are not saved in profiles. Named key files, hardware-backed keys, external data, caches and no-backup identity profiles/markers are excluded.

Replacement restore replaces the covered data folders while preserving existing local files and directories with excluded key-file names. Exclusions are filename based and recognize `.jks`, `.keystore`, `.p12`, `.pfx`, `.pem` and `.key` names. Restore archives cannot inject those excluded paths. Preservation is bounded and checked before replacement; unsafe paths, conflicting file types or limits cause restoration to stop rather than silently discard a local key.

ZIP merge preserves unrelated files. Single-file push uses an approved root and relative path. Archive paths, entry sizes and working limits are validated; a complete file backup is still not a snapshot of a running database. Close clone screens before transfers and restart after import or restore.

Runtime data transfers and document readers use cross-process leases. Conflicting imports, restores, cache cleanup, reset and restart are deferred or rejected while a runtime data operation is active. Source-app writes outside these tools can still occur.

**Show data in Android Files** is a separate read-only opt-in. It exposes approved roots through Android's document provider, independently of the Activity password gate. Writes go through the data tools.

## Feature coverage

The table below covers all **86 reference items** across 15 groups. The settings model contains **94 advanced fields and 72 legacy fields**. Configuration count and instruction-match count describe available controls and matched code locations; neither number establishes complete app coverage.

- **Available:** the described operation is implemented within its stated limits.
- **Scoped:** part of the request or selected APIs/views are supported.
- **Android controlled:** the result also depends on platform permissions, policy or device support.
- **Unavailable:** that function is not implemented in this release.

### 1. Identity and tracking

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| Change / Hide Android ID | Scoped | Replace selected Android ID reads with a chosen or generated per-clone value. The phone's own identifier and unsupported SDK paths remain unchanged. |
| Change / Hide IMEI & IMSI | Scoped | Replace selected IMEI and subscriber-ID getters. These settings do not modify radio hardware, system services or native identifier reads. |
| Change / Hide Wi-Fi & Bluetooth MAC | Scoped | Override selected Wi-Fi and Bluetooth MAC getters. Actual network-interface addresses and transmitted hardware addresses stay under Android's control. |
| Change Google Services Framework (GSF) ID | Scoped | Replace the Android-ID result of selected GSF provider queries. Google Play services, account identifiers and unrelated Google service data are not modified. |
| Change Advertising IDs | Scoped | Override selected Google advertising-ID, Amazon advertising settings and Facebook attribution queries. Other advertising SDKs and cached or server-side values can differ. |
| Hide SIM & Operator Info | Scoped | Mask selected operator, country, MCC/MNC, SIM-state and phone-type getters. This does not suppress all cellular metadata. |
| Randomize Build Props | Scoped | Generate a supported device profile or import allowlisted Build/OpenGL properties. Arbitrary system properties, kernel values and the device's build.prop file are unchanged. |
| Hide GPU & Display Info | Scoped | Override selected OpenGL vendor/renderer queries and display metric reads. Native graphics, Vulkan and other display APIs may reveal different information. |
| New Identity Preset | Available | Generate supported identifiers and a device profile, save the per-clone identity and restart the clone. Location and time-zone randomization are separate options. |

### 2. Privacy

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| Password Protection | Available | Protect Activity entry with a salted password, relock delay and optional supported biometrics. The password is a screen gate, not file encryption or protection for every background component. |
| Stealth Mode & Fake Calculator | Available | Use a working calculator launcher, enter the configured password and press equals to open the app. Long-press the display for text-password entry. Secret dialer codes are unavailable. |
| Panic Mode | Scoped | Use supported hardware-key or deliberate-shake exit actions. Notification controls can reset the clone. Hardware-key data wiping and arbitrary panic workflows are unavailable. |
| Incognito Mode | Scoped | Optionally reset after the last source Activity finishes, with active tools and data work deferred. Backgrounding, crashes and force-kills do not guarantee a reset. |
| Incognito Keyboard | Scoped | Request no personalized learning in standard text fields. The selected keyboard controls whether it honors Android's hint. |
| In-App Floating Keyboard | Scoped | Use an in-window keyboard for supported standard text fields and password dialogs, with a system-keyboard switch. Custom editors and privileged observers remain outside this control. |
| Remove / Spoof Permissions | Scoped | Remove individual or grouped manifest permissions and return empty results from selected provider/account calls. This does not emulate every permission grant or protected API. |
| Disable Hardware Sensors | Scoped | Suppress selected default-sensor and sensor-list queries. Native channels, previously acquired handles and unsupported sensor APIs remain outside this path. |
| Disable Access to Data Providers | Scoped | Restrict selected contacts, calendar, call-log and account reads. This is not a general firewall for every provider, write operation or alternate access path. |
| Disable Clipboard Access | Scoped | Suppress selected clipboard read, availability and description calls. Clipboard writes and unmatched or native access are not universally blocked. |
| Prevent / Allow Screenshots | Scoped | Request or clear capture protection on supported windows. Password and calculator entry stay protected. Android policy and secure video surfaces may still restrict capture. |
| Hide Root & Magisk | Scoped | Mask selected Java root-file, package, Build-tag and process-launch checks. Native detection, integrity checks and attestation are not comprehensively bypassed. |
| Hide Other Apps / Hide App Cloner | Scoped | Filter supported package lists, lookups and resolutions for chosen packages, other apps or known cloner packages. Android and other apps retain their own package visibility. |
| Disable Logcat Logging | Scoped | Suppress selected Android Log and console print calls. Native logging, diagnostics and independent crash-reporting libraries can still record information. |
| Exit Triggers | Scoped | Close clone screens on screen-off, app switching or a deliberate three-peak shake. System pickers and external sign-in flows can be affected by app-switch exit. |

### 3. Display

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| Color Customization | Scoped | Choose status/navigation, toolbar and notification colors with presets, RGB/opacity controls or hex entry. Apply styling to supported system bars, platform ActionBars and discovered Toolbars. Source themes, edge-to-edge rules and custom drawing can override the requested styling. |
| Dark Mode & Invert Colors | Scoped | Request clone-scoped night mode or an inverted content layer. The manager has a separate saved System/Light/Dark preference in Help. These controls do not change the phone's theme or guarantee recoloring of custom surfaces. |
| Modify Views | Scoped | Use the visible Find text and Replace with fields for literal, case-sensitive replacement in supported standard text views; editable and password fields are excluded. Hide exact matching text, resize standard text or apply opacity. An arbitrary view inspector and universal Compose/game editing are not included. |
| Window Sizing & Scaling | Scoped | Adjust supported density, language, font scale, text size and padding. Existing custom surfaces may not follow configuration changes; arbitrary window resizing is unavailable. |
| Multi-Window & Picture-in-Picture (PiP) | Scoped; Android controlled | Edit resizeable, PiP and task-reparenting declarations. Android and the source app must supply the actual window mode, transition behavior and device support. |
| Rotation Lock | Available | Request system, portrait, landscape, reverse or full-sensor orientation. Source behavior and Android large-screen policies may override the request. |
| Screen Behavior | Available | Request keep-screen-on, immersive bars, visible navigation bars and supported cutout behavior. Android's gesture and window policies remain authoritative. |

### 4. Mock options

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| Spoof Location | Scoped | Return configured coordinates from selected Location getters. Global providers, geofences, native coordinates and every fused-location path are not replaced. |
| Spoof GPS Track | Scoped | Interpolate a timed JSON route with bearing, accuracy and jitter. Routes support 2-1024 ordered points and up to seven days; GPX import and a system mock provider are unavailable. |
| IP-Derived Location | Scoped | Opt in to an HTTPS lookup that estimates coordinates from the clone's egress IP. The service sees that request, and the public IP itself does not change. |
| Hide Mock Location | Scoped | Return false from selected mock-provider/mock-location checks. Provider inconsistencies and other native or SDK detection methods may still be visible. |
| Fake Date & Time Zone | Scoped | Override selected Java wall-clock factories and time-zone paths. A configured zone also affects Java defaults. Scheduling clocks, OS time and native clocks remain unchanged. |
| Fake Environment Sensors | Scoped | Replace selected temperature, humidity and pressure event values. This does not create absent hardware or override every sensor channel. |

### 5. Media and audio

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| Audio Muting & Volume Override | Scoped | Mute selected MediaPlayer/AudioTrack calls or set foreground media volume, restoring its previous level after backgrounding. Native engines, SoundPool and unmatched paths may remain audible. |
| Mute Startup Sounds | Unavailable | No separate startup-only mute interval is provided. Supported-call muting applies beyond the startup period. |
| Prevent Audio Focus Theft | Scoped | Handle selected AudioManager focus calls without requesting system focus. This does not control every playback engine or Android focus decision. |
| Fake Camera / Dummy Audio Recorder | Scoped | Provide paced silent samples for selected AudioRecord calls. Construction still depends on Android permissions and hardware. Camera replacement and black-frame injection are unavailable. |

### 6. Navigation

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| Hardware Key Remapping | Scoped | Map delivered Volume Up, Volume Down and Assist events to Back, Home or Exit. Android may intercept keys first; screenshot and data-wipe key actions are unavailable. |
| Double-Back Behavior | Available | Use a second Back press within 1.5 seconds to minimize or exit. Arbitrary scripts and custom task workflows are not included. |
| Show Navigation Bar / Virtual Buttons | Scoped | Request software navigation bars or immersive hiding. A separate virtual-button overlay is unavailable, and Android controls navigation presentation. |
| Confirm on Exit | Available | Show confirmation for the configured Back action. Source-defined close buttons and OS process termination are not universally intercepted. |

### 7. Storage

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| Install to SD Card | Scoped; Android controlled | Request external installation with preferExternal. Android and device storage support decide placement; arbitrary data migration to an SD card is not performed. |
| Redirect External Storage | Unavailable | Shared external-directory calls are not redirected into a clone-private tree. Normal Android package-specific storage isolation still applies. |
| Accessible Data Directory | Scoped | Optionally expose approved files, preferences and databases through a read-only Android Files provider. It does not mount private app storage as a writable shared folder. |
| Disable Photo & Media Access | Scoped | Remove selected storage/media permissions. Existing URI grants, app-private files and explicit user-selected documents remain separate access paths. |
| Clear Cache on Exit | Scoped | Clean private cache after supported backgrounding, deferring for tools and data work. Manual cache clearing also checks code/external cache roots and reports deletion failures. |
| Bundle App Data | Available | Embed a validated initial-data archive for empty clone storage. Limits are 64 MiB total, 32 MiB per file and 10000 entries. Existing data is preserved by default. |
| Safe Update & Data Migration | Scoped | Update a clone with the same package and signing identity, or use scoped backup/import. Database schema changes and cross-app/account migrations remain the source app's responsibility. |

### 8. Launching

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| Exclude from Recents | Available | Request exclusion from Recents through manifest and own-task settings. The package remains visible in Android settings and other permitted system interfaces. |
| Disable Auto-Start | Scoped | Remove selected boot broadcast actions or disable declared components. Jobs, alarms, push delivery and every possible startup trigger are not universally disabled. |
| Hide App Icon / Decoy Launcher | Scoped | Remove launcher categories or use the calculator launcher. The manager can launch saved clones explicitly; secret-code/dialer launch paths are unavailable. |
| Auto-Launch on Device Events | Unavailable | Configurable USB, NFC, power-connect and storage-mount launch workflows are not provided. |
| Disable App Defaults | Available | Remove eligible non-MAIN default/browsable Activity filters. Existing Android roles and explicit intents are separate from these filter edits. |

### 9. Networking and proxying

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| SOCKS5 / HTTP Proxy Routing | Scoped | Configure one HTTP or SOCKS proxy, optional credentials and selected Java connection policies. Native networking, QUIC, DNS and unsupported clients can bypass these paths; no VPN is included. |
| Block Network Access | Available | Remove INTERNET permission to deny ordinary network access by that clone UID. The phone's connections and work delegated to another app are unaffected. |
| Disable Mobile Data / Background Networking | Scoped | Require Wi-Fi, foreground state or an existing VPN for selected Java requests. Open connections, native stacks and WebView internals are not a universal UID firewall. |
| WebRTC IP Leak Guard | Scoped | Disable JavaScript in supported WebViews to prevent their scripted WebRTC path. This can break pages and does not cover native WebRTC or all public-IP leaks. |
| App Cloner Tunnel Manager | Unavailable | App Cloner account integration, tunnel provisioning and a compatible hosted tunnel service are not included. |

### 10. Notifications

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| Notification Filter | Scoped | Filter selected notification posts by case-insensitive terms or bounded RE2 expressions. Filtered replacements cancel the previous ordinary notification; required service notifications receive generic content instead. |
| Notification Silence | Scoped | Silence supported notifications, apply quiet hours and reduce heads-up interruptions. Channels, user choices and unmatched posting paths remain under Android/source control. |
| Colorize / Badge Notifications | Scoped | Set supported notification accent colors, badge numbers and built-in small icons. LED behavior, launcher badge display and every channel setting are not guaranteed. |
| Hide Notification Content | Scoped | Replace supported notification content with generic/private content. Custom RemoteViews and unmatched notification paths require separate compatibility checks. |

### 11. WebView

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| Custom WebView User-Agent | Available | Apply a supplied user-agent string to discovered Android WebViews. It does not replace the browser engine or change native HTTP clients. |
| App Cloner Dedicated WebView | Unavailable | A separate proprietary or replacement WebView engine is not packaged. Android System WebView remains the browser component. |
| Clear Cache / Cookies on Exit | Scoped | After supported backgrounding, clear discovered WebView cache/history/form data and process cookies/DOM storage. Crashes, force-kills and other browser engines are outside this guarantee. |
| Disable JavaScript / DOM Storage | Scoped | Disable JavaScript or DOM storage in discovered WebViews; matched JavaScript-enable calls honor the guard. Source pages can stop working when these options are enabled. |

### 12. Automation

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| Auto-Press Buttons | Scoped | Click a visible exact standard-text match, with limited parent traversal and once-per-foreground tracking. OCR, cross-app automation and system-dialog workflows are unavailable. |
| Auto-Scroller | Scoped | Scroll supported unlocked foreground views at a configured interval. Custom feeds, canvases and other apps are not universally supported. |
| State Controls on Launch | Scoped; Android controlled | Request launch brightness, media volume, torch, DND, Wi-Fi and Bluetooth changes through permitted APIs or system consent. Supported temporary torch/volume/DND changes are restored after backgrounding. |

### 13. Manifest and resources

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| XML Manifest Editor | Available | Edit/import a bounded source-compatible manifest before clone transformations. Invalid edits can break the source app; custom entities/DOCTYPE and unsafe structures are rejected. |
| App Translator | Scoped | Replace existing named strings through JSON or plain strings.xml, across matching locales. Nested markup, plurals and arrays are rejected; automatic translation is unavailable. |
| Target / Min SDK Modifier | Scoped | Change SDK declarations while preserving required legacy defaults. Runtime clones require API26+. A lower declaration neither supplies missing APIs nor bypasses installation or permission policy. |
| Component Manager | Scoped | Disable selected declared activities, aliases, services, providers or receivers. Removing an override preserves source behavior; enabling every source-disabled component is not supported. |

### 14. Developer options

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| Custom Build Props File | Scoped | Import bounded JSON or UTF-8 key=value properties from the validated Build/OpenGL allowlist. Unsupported keys, duplicates and oversized input are rejected; arbitrary OS property replacement is unavailable. |
| App Info Service | Unavailable | The protected manager bridge can report clone storage usage. A public external automation API for general app, proxy, IP or GPS status is not provided. |
| Skip Native Libraries | Available | Keep selected native ABI directories and remove others. Absent-only selections are rejected. Native code is not recompiled or made compatible with a different CPU. |
| Disable Crash Dialogs | Unavailable | Global OS crash/ANR-dialog suppression is unavailable. Source crashes still require compatibility fixes in the affected application. |

### 15. Core cloner and batch builds

| Feature | Coverage | Behavior and limits |
| --- | --- | --- |
| Batch Cloning | Available | Validate and build up to 20 numbered clones sequentially. Cancel stops at a processing boundary and preserves already completed builds. |
| Clone Number Badging | Available | Add a clone-number badge to the generated launcher icon. Final masking and adaptive-icon presentation depend on the launcher. |
| Icon Modifier | Available | Choose a custom image, change hue, invert colors or flip the generated launcher icon, with Original/Clone live previews using the export renderer. Source-driven dynamic icon changes and all launcher behaviors are not rewritten. |
| Google Maps Support Add-on | Scoped | Replace Maps key metadata with a key from a project you control. Its package/certificate restrictions must authorize the clone; automatic third-party key authorization is unavailable. |
| Save / Export Clone APKs & Profiles | Available | Export/share signed APKs, library APK ZIPs and JSON profiles. Install uses a temporary APK read grant and Android confirmation. App-data backup is separate; private signing keys are not exported. |

## Import and operating limits

| Item | Limit or condition |
| --- | --- |
| Input archive | Up to 512 MiB |
| Prepared APK | Up to 256 MiB |
| Split packages | Up to 128 matching APKs |
| ZIP entries | Up to 20000 |
| Batch | Up to 20 sequential clones |
| Initial-data archive | 64 MiB total, 32 MiB per file, 10000 entries |
| Runtime-equipped clone | Android 8.0 / API26 or newer |

Split signatures, package versions, dependencies, checksums, duplicate classes and file conflicts are checked. Unsafe archive paths, ambiguous multiple-base sets, unsupported overlays, shared-user packages and OBB expansion files are not supported. An input within these limits can still exceed a particular device's available memory or storage.

Package and signature changes can break sign-in, billing, DRM, integrity checks, provider references and app-specific service restrictions. Native code, reflection, dynamically loaded code, framework-internal calls and alternative SDKs can bypass selected rewrites. Standard-view controls do not imply universal support for Compose, Flutter, games, canvases or video surfaces.

No system WebView replacement, hosted App Cloner tunnel, camera-stream replacement, startup-only mute interval, screenshot/data-wipe key action, device-event launch engine, public app-status API or shared-directory redirection is included. The feature table gives the scope of related controls.

## Privacy and signing

The manager has no Internet permission and sends no analytics. APKs, sources, icons, profiles and history remain in its private storage until exported or shared. Optional IP-derived location sends a request from the clone to the selected HTTPS service.

The APK that installs Undercover App Cloner and the APKs it generates have separate signing roles. This distribution uses the owner's **UITF** signing identity for the manager. The manager creates its clone-signing key in AndroidKeyStore on the device. Neither that private key nor the UITF keystore/password is distributed in this repository.

Android requires the same compatible signing identity for manager updates. This UITF release does not use a rotation lineage from the previous development certificate. The migration note above applies to those older manager installations. Clone data restore can preserve existing excluded local key files, but it cannot export or recover the manager's AndroidKeyStore signing key or restore hardware-backed clone keys.

A clone password protects app entry. It does not encrypt the clone's files or APK configuration. Exported profiles and generated APK settings can contain configured proxy credentials, so handle those files as private configuration.

## Verification and compatibility

The v0.6.0 release assembly succeeded. Its fresh release-variant host test run passed **248 tests**: 102 manager tests and 146 runtime tests, with zero failures, errors or skipped tests. Full lint completed with **zero errors**, 19 manager warnings and 62 runtime warnings.

The host tests cover compiled fixture APK transformations, manifest/resource edits, settings validation, selected DEX calls and fields, runtime contracts, identity persistence, notification rules, clocks, file containment, archive encryption, restore recovery and data-operation coordination. Tests also cover literal text replacement, ad/tracker host rules, preservation of excluded local key files and rejection of archive key injection. Host tests do not execute every Android UI or hardware path.

Native Android 9 verification on the 0.6.0 debug build passed **13 icon checks** using Android Bitmap and Canvas. These included full-pixel preview/export equality, hue-zero identity, inversion, alpha, both flips, batch suffixes, number badges and source-image preservation. Actual manager screens also confirmed Light and Dark selection, Dark persistence after restart, and visibility of the System choice. Following device night-mode changes was not completed. These checks cover the named paths only.

The final signed-APK update test was blocked when the Android 9 emulator lost its activity and package services. It did not confirm a 0.5.0-to-0.6.0 update or a launch of the delivered release APK. Interactive checks of the text, color and ad controls on that APK remain outstanding. This system failure was not a reproduced manager crash.

Historical Android 15 checks on earlier 0.4.0 verification builds covered local AndroidKeyStore cloning/signing, selected identifier/location/time-zone paths, encrypted backup/restore, file push/export, cache clearing, temporary-URI revocation, protected data access, notification filtering, identity rotation and own-data deletion. An earlier real Library Install update reached Android's **App installed** result and returned to Library with the same manager process. These observations belong to those earlier builds, not to this newly branded UITF-signed APK.

**Android 16 and 17 end-to-end compatibility is unverified.** The earlier emulator checks were blocked by operating-system service failures before the manager UI could be tested, and the reported phone-side Install crash was not reproduced. The Android 9 checks above do not establish compatibility on newer phones. Biometric, persistent document-grant and keyboard-viewport paths still require matching device checks. Physical phones, OEM installer policy, persistent document grants and source-app/API combinations need matching device checks.

Use the exact APK version and SHA-256 above when reporting a problem. Include the Android version, source app/package, selected settings, action taken and the error or crash log where available. A successful build or signature check does not establish that every source app or option combination will work.

## Credits

Undercover App Cloner is developed by **Sharodshahi Al-Amin**, owner of **Undercover IT Firm**. The in-app About page provides release information and developer contacts.

- [Telegram](https://t.me/savaskarofficial)
- [GitHub](https://github.com/savaskarofficial)
- [Undercover IT Firm website](https://undercoveritfirm.com)

Third-party components retain their respective copyright and licence terms. See [Third-party notices](THIRD_PARTY_NOTICES.txt).
