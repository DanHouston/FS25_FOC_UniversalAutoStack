# FS25_FOC_UniversalAutoStack (fork)

This repository is a fork of the original `FS25_UniversalAutoload` mod adapted to support manual implement-based auto-stacking.

Overview
- The original mod provided automatic loading from ground objects into trailers. This fork changes the behaviour so that pallets and other stackable objects can be collected by a forklift/implement (mounted), then automatically stacked onto a trailer when the implement brings the items to the trailer's loading trigger.
- Key goals achieved so far:
	- Manual collection: mounted/implement-held items that enter the trailer auto-trigger are detected along with the rest of the stack on the implement.
	- Group-aware queuing: the fork collects the full mounted/stacked group, adds them to the vehicle's available queue, and invokes the existing autoload placement logic so stacking order and placement are consistent with ground autoload.

Why this fork exists
- The original mod provided a high level of automation that could place items without realistic player interaction. This fork intentionally reduces that automation to make stacking behaviour more realistic and predictable.

- Instead of fully automatic ground-based loading, this fork requires the player to collect pallets with an implement (e.g. forklift) and bring the stack to the trailer. When the implement's pallet contacts the trailer trigger the mod detects the full mounted/stacked group and assists by queuing those items into the trailer's normal placement flow.

- The goal is to simplify and assist realistic stacking onto trailers while keeping the player in control — not to reintroduce or increase fully automated loading.

Usage / Testing Notes
- Install and enable the mod as usual.
- To test manual stacking:
	1. Spawn or prepare a few pallets and mount them on a forklift/implement.
	2. Drive the implement so the stack's lower pallet touches the trailer's auto-loading trigger (side/rear auto trigger).
	3. The mod will now attempt to detect the full stack, queue the objects, and start loading using the standard placement algorithm.

Current Limitations and Next Work
- Retry behaviour: currently the code collects the full stack and queues the objects into `availableObjects` and starts loading. Improvements remaining:
	- Retry-on-failure: do not drop queued items when a placement fails; instead keep them for later retry (planned).
	- Tighter spatial filtering: adjust trigger-area scanning to avoid false positives in crowded scenes (optional tuning).

Code locations of interest
- Trigger callback and collection changes: `UniversalAutoload.lua` — see `ualAutoLoadingTrigger_Callback` and new `collectMountedStack()` helper.
- GUI strings: `gui/ShopConfigMenuUALSettings.xml` uses localization keys located in `language/l10n_*.xml` (e.g. `language/l10n_en.xml`).

Credits
- Original mod by the upstream `FS25_UniversalAutoload` project. This fork (FS25_FOC_UniversalAutoStack) adapts the code for manual implement-based stacking behaviour.

- Original mod repository: https://github.com/loki79uk/FS25_UniversalAutoload
