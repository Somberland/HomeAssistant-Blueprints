# 🏠 HomeAssistant Blueprints

A collection of Home Assistant automation blueprints for smart lighting control.

**Author:** Phil Skorpil · [GitHub @Somberland](https://github.com/Somberland)
**Repository:** [github.com/Somberland/HomeAssistant-Blueprints](https://github.com/Somberland/HomeAssistant-Blueprints)

---

## 📦 Available Blueprints

### 1. 💡 Timeslot Light Control v1.7 (`timeslot-light.yaml`)

> Trigger-based light automation with a 24/7 fallback, up to 5 configurable time windows with individual light settings per slot, and optional Fade-In / Fade-Out transitions.

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/Somberland/HomeAssistant-Blueprints/blob/main/timeslot-light.yaml)

#### Features

| Feature | Details |
|---|---|
| **Trigger** | Binary Sensor (motion, door, etc.) or Schedule helper |
| **Light targets** | Entities, Areas (rooms) and/or Devices — all in one selector |
| **Default / Fallback** | 24h fallback settings when no time slot is active (on by default) |
| **Time slots** | Up to 5 independent time windows (e.g. 18:00–23:00) |
| **Per-slot settings** | Brightness (%), Color Temperature (K), or RGB color |
| **Lux sensor** | Only activate when below lux threshold; optional brightness boost in darkness |
| **Fade-In** | Soft ramp-up from 0 → target brightness (configurable duration) |
| **Fade-Out** | Soft ramp-down to 0 before turning off (configurable duration) |
| **Off delay** | Configurable delay before turning off after trigger clears |

#### How It Works

1. **Trigger activates** (sensor turns ON or schedule starts)
2. Blueprint checks **which time slot is currently active**
3. If a slot is active → lights turn on with that slot's settings (+ optional Fade-In)
4. If **no slot is active** → fallback settings are used if enabled (default: on)
5. If a **lux sensor** is configured → light only turns on when lux is below the threshold
6. **Trigger clears** → lights turn off after the configured delay (+ optional Fade-Out)

> **💡 Tip – Gaps between time slots:** If the fallback is disabled and no slot is active, triggers are silently ignored — the light won't turn on. Use this intentionally as a **block period** (e.g. no motion activation during daytime).

#### Configuration

<details>
<summary><b>🎯 Trigger Settings</b></summary>

- **Trigger Entity** *(required)*: One or more `binary_sensor` or `schedule` entities
- **Off Delay**: How long to keep lights on after trigger clears (0–60 minutes)

</details>

<details>
<summary><b>💡 Light Settings</b></summary>

- **Light Targets** *(required)*: Select lights by entity, area (room), or device — mix and match freely

</details>

<details>
<summary><b>☀️ Lux Sensor (Optional)</b></summary>

Adds ambient light awareness to the automation:

| Setting | Description |
|---|---|
| Enable | Toggle lux control on/off |
| Lux Sensor | Any `illuminance` sensor entity |
| Max threshold | Don't turn on if lux is **above** this value (default: 200 lx) |
| Brightness boost | Optionally increase brightness when lux is very low |
| Boost threshold | Apply boost when lux is below this value (default: 30 lx) |
| Boost amount | How much to add to the slot brightness, capped at 100% (default: +30%) |

</details>

<details>
<summary><b>🌟 Default / Fallback Settings</b></summary>

Used when no time slot is currently active. Enabled by default — this makes the blueprint work out of the box without configuring any time slots.

- **Enable/Disable**: Toggle the fallback on or off
- **Brightness**: 1–100 %
- **Color Mode**: Color Temperature (K) / RGB / Brightness only
- **Color Temp**: 2000–6500 K
- **RGB Color**: Full color picker

</details>

<details>
<summary><b>🌅 Fade In / Fade Out (Optional)</b></summary>

- **Fade-In**: Enable smooth turn-on transition; set duration in seconds (1–60 s)
- **Fade-Out**: Enable smooth turn-off transition; set duration in seconds (1–60 s)

</details>

<details>
<summary><b>⏰ Time Slots 1–5 (each Optional)</b></summary>

Each of the 5 time slots can be independently configured and takes priority over the fallback:

| Setting | Description |
|---|---|
| Enable/Disable | Toggle the slot on or off |
| Start Time | e.g. `18:00` |
| End Time | e.g. `23:00` |
| Brightness | 1–100 % |
| Color Mode | Color Temperature (K) / RGB / Brightness only |
| Color Temp | 2000–6500 K (slider) |
| RGB Color | Full color picker |

</details>

#### Example Use Cases

- **Simple 24/7**: Just enable the fallback, set brightness/color — done. No time slots needed.
- **Evening ambiance**: 18:00–23:00 → 50% brightness, 2700 K warm white
- **Morning boost**: 07:00–09:00 → 100% brightness, 5000 K cool white
- **Night mode**: 23:00–00:00 → 10% brightness, 2200 K very warm

---

## 📥 Installation

### Option A – Import via URL (recommended)

Click the **Import Blueprint** badge above, or go to:

**Home Assistant → Settings → Automations & Scenes → Blueprints → Import Blueprint**

Paste the raw GitHub URL of the desired `.yaml` file.

### Option B – Manual installation

1. Copy the `.yaml` file into your Home Assistant config directory:
   ```
   config/blueprints/automation/<your-folder>/timeslot-light.yaml
   ```
2. Reload blueprints in Home Assistant (Developer Tools → YAML → Reload Blueprints)
3. Go to **Settings → Automations → + Create Automation → Use a Blueprint**

---

## 🤝 Contributing

Pull requests and suggestions are welcome! Please open an issue first for larger changes.

---

## 📄 License

MIT License – free to use, modify and share.
