# Changelog

## 1.6.2

- Fixed conflicting device identities: the manager's old Pixel-only generator no longer pins Google properties and Mali GPU values over a selected company/model. Catalog identity settings now replace stale manual profile properties.
- Added an explicit Randomize RAM and processor switch. New identity saves another independent hardware test configuration and restores it after restart; fixed and Original hardware settings remain available when the switch is off.
- Added the effective device and hardware summary to the controls notification and action screen.
- Added strictly matched Java FileReader support for bounded memory/CPU read views, including selected /proc and CPU state/frequency paths. Native calls, unmatched paths and actual kernel files are unchanged.
- Clarified catalog and manual Build-property modes so applying one does not silently retain contradictory settings from the other.

Rebuild existing clones from their original source APK to receive these runtime changes. The hardware configurations are independent test values, not verified factory specifications for the selected phone.

## 1.6.1

- Replaced the library's direct installer handoff with streamed Android PackageInstaller sessions. Installer-service work runs off the main thread, with progress, pending-session recovery, cancel/retry controls and Export available during installation.
- Added local install diagnostics with view, copy and save actions, recorded install stages and available Android exit information.
- Added 500 company/model identities with search, fixed selection and company-filtered random profiles. Separate validated RAM, CPU-core and processor overrides apply to selected Java API paths; native and physical hardware values are unchanged.
- Added GPX import for a single continuous timed or untimed track/route, using the existing bounded location-route validation.
- Added a startup-only mute interval for supported MediaPlayer and AudioTrack calls, with requested-volume restoration.
- Added movable Back, Home and Close buttons inside the clone, with lock-state guards and close confirmation.
- Added clone-private redirection for selected Environment shared-storage directory getters.
- Added a searchable resource-string editor with draft changes, original-value restoration and JSON/XML import.

Clone runtime changes require rebuilding and installing the generated clone. The new controls have explicit API and platform limits; they do not make every source app compatible.

## 1.6.0

## What changed

- **Live icon preview:** Open **Identity > Icon adjustments** to see hue, inversion, flips and the clone-number badge before building. The preview and exported icon use the same renderer.
- **Clear text replacement:** Under **Options > Display**, both **Find text** and **Replace with** stay visible. To change `Test` to `Testuuu`, enter those two values. A preview appears below them.
- **Color picker:** Status bar, navigation bar, toolbar and notification accent colors now have presets, RGB and opacity sliders, hex entry and an Original option.
- **App appearance:** Open **Help > App appearance** and choose System, Light or Dark. The choice is saved and applies to the manager, including its data dialogs.
- **Ads and tracking:** A dedicated category provides known ad-domain and tracker-domain filters, plus up to 256 custom domains. The included lists are stored locally.

Existing clones need to be rebuilt and installed to receive new clone settings. Changing the manager's appearance takes effect immediately.

