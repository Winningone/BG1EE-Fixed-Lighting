# Fixed Lighting for BG1EE — 0.1.0 prototype

Keeps the appearance of outdoor areas fixed while the game clock continues
to advance. Temporary character effects are not patched or rescheduled.

## Status and coverage

This is a development prototype, not an in-game-tested release.

* **Fixed daylight:** clears the day/night and extended-night flags on
  outdoor ARE V1.0 resources which originally had a day/night cycle.
* **Fixed native night artwork:** experimental. Uses a private copy of each
  area's existing night WED and night light map as its non-cycling map.
  Areas without those resources are **skipped** and retain their normal cycle.
  Thus this option does **not** deliver permanent night across all of BG1EE.
  The installer prints each changed and skipped area into its debug log.

Night coverage must be measured against your installed game. Areas using only
engine tinting need additional work; no invented night graphics are supplied.
Maps inside archives which WeiDU cannot see will not be patched.

The clock, calendar, NPC schedules, quest timers, rest, travel, and encounter
times continue to operate. Time-scheduled lamps and other area animations,
music, and sounds can still change with time. Interiors retain their existing
appearance. Changing light maps may affect hiding and infravision; this is
not guaranteed to be purely cosmetic to every mechanic.

## Windows installation

1. Close the game. Keep a copy of a save made before installing for testing.
2. Extract the ZIP into the BG1EE game folder containing `chitin.key`.
   The `fixed-lighting` folder and `setup-fixed-lighting.exe` should be directly
   in that folder, not inside a second enclosing ZIP folder.
3. Run `setup-fixed-lighting.exe` and choose one lighting component.
   If the EXE is not included, download Windows WeiDU from
   https://github.com/WeiDUorg/weidu/releases, copy `weidu.exe` here, and rename
   it to `setup-fixed-lighting.exe`.
4. Install after other mods which add or change areas. Review the debug log
   for skipped night areas and errors.
5. Start a new temporary game for the first test. Previously visited areas
   can be cached in existing saves, so this does not reliably update them.

Linux/macOS: place a WeiDU binary in the game folder and run
`weidu fixed-lighting/setup-fixed-lighting.tp2`. Platform-specific filesystem
setup may be required; Windows is the primary target of this package.

## Test before using for a full playthrough

1. In a new temporary game, visit an outdoor map during daytime and nighttime.
   For daylight, verify both use the same daylight artwork and character tint.
   For night, test an area listed as changed, plus one listed as skipped.
2. Cast a short timed spell such as Shield. Leave the game unpaused and confirm
   that it expires at its normal duration. Confirm poison or another temporary
   condition also expires normally, if available.
3. Rest, travel, save, and reload. Verify the chosen artwork is retained and
   the game clock advances. Check doors, water, actor tint, map display, and
   lights for visual problems.
4. Confirm a time-scheduled NPC still appears at the normal hour.
5. Uninstall using the installer and repeat with a pre-install save or a new
   game. Do not delete the backup directory before uninstalling.

Switch lighting modes by rerunning the installer and selecting the other
component. The two components are mutually exclusive. An existing save may
still contain its old area state after either switching or uninstalling.

## Implementation and sources

No DayNight actions, clock resets, time-stop spells, game executable changes,
or modifications to SPL/CRE/EFF duration fields are used.

Documented ARE V1.0 area type at 0x48: bit 0 outdoor, bit 1 day/night,
bit 6 extended night. Mask 0xffbd clears bits 1 and 6.
https://gibberlings3.github.io/iesdp/file_formats/ie_formats/are_v1.htm

Effects can store an expiration tick in the advancing game clock:
https://gibberlings3.github.io/iesdp/file_formats/ie_formats/eff_v2.htm

WeiDU installation, patch syntax, and subcomponents:
https://weidu.org/~thebigg/README-WeiDU.html

Night auxiliary-map naming was cross-checked against GemRB's AREImporter,
an open-source reimplementation. This is supporting evidence, not a test of
Beamdog's engine; night resource loading still requires BG1EE verification.
https://github.com/gemrb/gemrb/blob/master/gemrb/plugins/AREImporter/AREImporter.cpp

Only your local installed game assets are copied by the installer. The package
does not redistribute BG1EE artwork. WeiDU is developed by its own maintainers;
its licensing and distribution information is in WEIDU-NOTICE.txt if bundled.
