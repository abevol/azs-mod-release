# AZS — Azerothian Zenith Suite

[中文](README.md) | **English**

A local gameplay mod for *Azeroth Survivors*: takes the growth caps off their
fixed marks and hands the calibration to the player.

The Titans set order upon Azeroth and measured out what its children may
become — level 99, 51 talent points, fixed quality and cooldowns. This
"suite" unscrews the zenith from those fixed marks and lets you recalibrate.

![AZS in-game settings panel](mod.png)

> This mod only alters the local single-player experience — no networking, no
> shared data. Use of third-party mods is at your own risk; if a game update
> breaks it, come back here for a new build.

## Features

| Feature | Description | Vanilla | Range |
|---|---|---|---|
| Run level cap | The XP bar keeps going past level 99 | 99 | default 200, configurable |
| Talent point cap | Break past the structural 51-point limit | 51 | default 100, 3–127 |
| Lucky quality floor | With enough luck, low qualities stop dropping | — | 60/90/140%, can disable |
| Cooldown display | Upgrade cards show each spell's cooldown on the first line | — | on/off |
| Battle speed | Speeds up in-run game time at the selected tier (movement, cooldowns, spawns); the top bar switches tiers instantly and resets to x1 in the lobby | 1x | default 1/2/5/10, four tiers configurable 0.1–20 |
| In-game settings panel | MODS → AZS; "Apply" takes effect immediately, writes back the config, and closes the panel | — | — |
| Launcher self-update | Checks for a new release on startup and applies it, trying gh-proxy → ghfast → ghproxy → direct download (failures never block launch); `--no-update` skips | — | — |

The panel follows the game's interface language: Chinese for zh locales,
English otherwise.

## Installation

1. Download `azs-mod-v0.3.1.zip` from the **Releases** page and extract it
   anywhere:
   - `azs-launcher.exe` (the launcher, which injects the mod)
   - `azs_mod.dll` (the mod itself)
   - `azs-mod.toml.example` (config template)
2. Rename `azs-mod.toml.example` to `azs-mod.toml` (optional — without it the
   mod uses built-in defaults).
3. **Run `azs-launcher.exe` to start the game** (do not launch the game exe
   directly — the mod is injected by the launcher). You pick the game path on
   first run; it is remembered afterwards. The in-game panel (AddOns) is
   installed into the game folder by the launcher automatically.

## In-game panel

Open **MODS → AZS** on the right side of the screen. Common adjustments
(caps, luck thresholds, cooldown toggle, battle-speed switch and the four
tiers) need no file editing: press "Apply" and the change takes effect
immediately, writes back to `azs-mod.toml`, and the panel closes.

With battle speed enabled, a bar appears at the top of the screen (slightly
right of center) while in a run — default x1/x2/x5/x10, click a tier to apply
it instantly. Returning to the lobby resets the game to x1 and hides the bar;
the selected tier is applied again on the next run. **Keep x1 in co-op**:
different speeds on the two ends will desync.

## Configuration

`azs-mod.toml` is a runtime file (rewritten when you apply settings in-game).
Without it the following built-in defaults apply:

```toml
log           = false  # diagnostic log; set true when troubleshooting
run_level_cap = 200    # run level cap (vanilla 99)
talent_cap    = 100    # talent point cap (vanilla 51)

luck_quality  = true   # lucky quality floor (on by default)
luck_t1       = 60     # >=60%: no Common drops
luck_t2       = 90     # >=90%: no Uncommon or below
luck_t3       = 140    # >=140%: no Rare or below

cooldown      = true   # upgrade cards show the spell cooldown on the first line

speed         = true   # battle speed (off forces x1 and hides the top bar)
speed_tier    = 1      # current tier 1–4
speed1        = 1      # the four multipliers; editable in the panel
speed2        = 2
speed3        = 5
speed4        = 10
```

`talent_cap` should be a multiple of 3 (talents are granted 1 point per tree
per tier).

## Game auto-update

The game's built-in updater starts a new process and then exits the old one.
The launcher watches for a same-named process while the game runs and injects
the mod DLL into the new one, so **the mod survives update restarts** — no
need to double-click the launcher again.

If the game restarts with administrator rights, the launcher needs them too.

## License & disclaimer

This repository contains build artifacts only, for personal use. The mod is
not affiliated with *Azeroth Survivors* or its developers; any loss caused by
using it is on you.
