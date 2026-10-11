# BG1EE Fixed Lighting

Experimental WeiDU mod for Baldur's Gate: Enhanced Edition. It aims to keep outdoor lighting fixed while the game clock advances normally, allowing timed character effects to expire.

**Prototype status:** installer changes and uninstall restoration were checked with synthetic test resources. The mod has not been tested inside BG1EE on Windows or macOS. Permanent night has partial map coverage.

## Download

[Download BG1EE-Fixed-Lighting-v0.1.0.zip](BG1EE-Fixed-Lighting-v0.1.0.zip?raw=true)

Use this ZIP for installation. GitHub's **Code → Download ZIP** downloads the source repository and does not place the Windows installer directly in your game folder.

## Options

- **Fixed daylight:** disables the lighting cycle in eligible outdoor areas.
- **Fixed native night artwork:** experimental; only changes maps with existing night artwork and light maps. Unsupported maps retain their normal cycle and are listed in the installer log.

The clock, NPC schedules, quest timers, rest, and travel continue to advance. Scheduled lights, sounds, and music may still change. Light-map changes may affect hiding and infravision.

## Windows

1. Close BG1EE and keep a pre-install save.
2. Extract the downloaded mod ZIP into the game folder containing `chitin.key`.
3. Run `setup-fixed-lighting.exe` and select one lighting option.
4. Test with a new temporary game first; previously visited areas may be cached in existing saves.

## macOS — unverified

The included EXE is Windows-only. The mod source is expected to be usable with Mac WeiDU, but actual Mac installation and gameplay are unverified.

1. Download the appropriate binary from [WeiDU 251](https://github.com/WeiDUorg/weidu/releases/tag/v251.00): **WeiDU-Mac-251.zip** for Intel or **WeiDU-Mac-ARM-251.zip** for Apple silicon.
2. Put the Mac `weidu` binary and this mod's `fixed-lighting` folder in the writable game data directory containing `chitin.key`.
3. Open Terminal in that directory and run:

```bash
chmod +x ./weidu
./weidu fixed-lighting/setup-fixed-lighting.tp2
```

Game-folder layout and macOS security prompts can differ by installation. These commands assume the binary is named `weidu` and is in the current directory.

## Uninstall

Rerun the same installer and select **Uninstall**. Keep the `fixed-lighting/backup` directory until uninstall is complete. WeiDU restores changed files and removes the private night resources.

Existing saves may retain modified area data. Return to a pre-install save or start a new game if lighting remains altered after uninstalling.

## Test checklist

- Confirm the selected lighting stays fixed through rest, travel, save, and reload.
- Confirm a short timed spell such as Shield expires normally.
- Check doors, water, character tint, and map display.
- Confirm uninstall restores the original behavior using a pre-install save or new game.

See [full instructions](fixed-lighting/README.md) and [validation details](fixed-lighting/VALIDATION.md).

## Source and third-party software

The WeiDU installer source is [fixed-lighting/setup-fixed-lighting.tp2](fixed-lighting/setup-fixed-lighting.tp2).

The mod ZIP includes an unmodified Windows WeiDU binary. Its license and attribution are included in [WEIDU-COPYING.txt](WEIDU-COPYING.txt) and [WEIDU-NOTICE.txt](WEIDU-NOTICE.txt). No BG1EE artwork is distributed; the installer copies resources from the user's own game installation.
