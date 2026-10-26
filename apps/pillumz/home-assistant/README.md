# Home Assistant

A native Omalauncher app for a Home Assistant server. It discovers areas and entities instead of requiring a hand-written dashboard.

## Features

- Favorites on the opening page, or an automatically discovered room list until favorites are chosen.
- Room detail views with lights, covers, and favorite read-only sensors.
- Light toggling, room-wide lights-off, and brightness when supported.
- Cover open/stop/close and position when supported.
- Multiple to-do lists, quick-add, completion, editing, due dates, and deletion with confirmation.
- Persistent favorites, hidden entities, room order, selected list, and cached data for offline reads.
- Clear pending, unavailable, offline, and error states.

## Connection

The app uses a small Python helper in Omalauncher's optional Arch Linux environment. Its **Connect Home Assistant** action opens a guided terminal setup: enter the server URL, paste a long-lived access token into a hidden prompt, and test the connection before saving. No configuration-file editing is required.

The configuration is compatible with Simon Schubert's Home Assistant widget: `~/.config/omarchy-proot/home-assistant`, with the URL on line 1 and token on line 2. The file is mode 0600 and is never embedded in the app or its persisted OWL state. Entity IDs are discovered automatically; any lines after the token are ignored by this app.

Both HTTP and HTTPS are supported. HTTPS is recommended because HTTP does not encrypt the token or traffic in transit. Changing servers reruns the same guided setup without losing favorites or display preferences.

## Design contract

- Simon Schubert's OWL apps are the primary UI reference: bottom navigation, compact margins, hairline dividers, quiet foreground-alpha surfaces, theme-scaled corners, dynamic titles, Back behavior, haptics, and cached offline data.
- Home and Tasks are the two top-level destinations. Settings and detail views use Back.
- Tapping a light toggles it. Its expand control reveals brightness inline. Covers always expand to explicit controls rather than toggling accidentally.
- The app adapts to discovered capabilities rather than showing unsupported controls.
- All colors and corner choices follow the active Omarchy theme. Touch targets remain generous despite the dense presentation.

## Development and review

The app is self-contained in `app.owl`; the Python helper is embedded and installed into the user's data directory. It uses only Python's standard library and requires the `python` package.

Development uses a fictional local HA-compatible server, an Android emulator, and no production credentials or devices. Store checks:

```sh
java -jar tools/owl.jar check apps/pillumz/home-assistant/app.owl
java -jar tools/owl.jar review . apps/pillumz/home-assistant/app.owl
```
