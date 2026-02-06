# Atmospheric Weather Card

> **AI-DISCLAIMER:**
> This card was created with the help of AI.

A custom Home Assistant card that renders beautiful, animated weather effects. It features organic clouds, realistic rain/snow physics, suspended particles, and dynamic lighting.

## Usage Modes

This card is designed to be versatile and can be used in two distinct modes depending on your dashboard design.

### 1. Standalone Mode (New in v1.7)
**"The Plug-and-Play Card"**
* **What it does:** Operates as a standard Lovelace card with its own background, rounded corners, and shadow.
* **Visuals:** Renders gorgeous, dynamic gradients that change based on the weather (e.g., Deep Grey for storms, Sky Blue for sunny days, OLED Black for night).
* **Data:** Automatically displays the current temperature and location text directly on the card.
* **Best for:** Section views, grids, and standard dashboards where you want a weather card that just works.

### 2. Immersive Mode
**"The Infinite Canvas"**
* **What it does:** Renders with a **transparent background**.
* **Visuals:** Designed to be placed *behind* other elements or used in a `picture-elements` card. It acts as a living "atmosphere" layer for your dashboard.
* **Data:** Displays animations only (no text), allowing you to overlay your own buttons or sensors.
* **Best for:** Your Dashboard Header, Heavily customized dashboards or layering behind a transparent image of your house.

---

## Table of Contents

* [Screenshots (Standalone Mode)](#screenshots-standalone-mode)
* [Screenshots (Immersive Mode)](#screenshots-immersive-mode)
* [Screenshots (The Complete Scene)](#screenshots-the-complete-scene)
* [Technical Features](#technical-features)
* [Installation](#installation)
* [Configuration](#configuration)
* [Feature Documentation](#feature-documentation)
* [Custom House Image Generation](#custom-house-image-generation)
* [Adding Buttons](#adding-buttons)

---

## Screenshots (Standalone Mode)


<img width="407" height="151" alt="image" src="https://github.com/user-attachments/assets/be96819b-923a-414d-8bd6-414b2a80cded" />
<img width="386" height="126" alt="image" src="https://github.com/user-attachments/assets/4b63e40a-286e-48d6-b0e3-e2095493cfd7" />



## Screenshots (Immersive Mode)

| Day | Night |
| :---: | :---: |
| **Partly Cloudy** <br> <img src="https://github.com/user-attachments/assets/ff05d0f2-87d2-4dd9-9253-e1fa99d7c7b7" width="100%" alt="Day - Partly Cloudy" /> | **Stormy Weather** <br> <img src="https://github.com/user-attachments/assets/efb3ed85-16c2-494c-bc10-65c3006b2c6f" width="100%" alt="Night - Stormy" /> |
| **Windy Weather** <br> <img src="https://github.com/user-attachments/assets/9e2606a7-5838-4d32-9031-f95dc0f03fe4" width="100%" alt="Day - Windy" /> | **Partly Cloudy (a Comet!)** <br> <img src="https://github.com/user-attachments/assets/814dc888-2601-4c3c-91c5-a9ff6bcdc578" width="100%" alt="Night - Comet" /> |
| **Rainy Weather** <br> <img src="https://github.com/user-attachments/assets/0fa2a2eb-d869-4d84-a6aa-b0b1999d49ea" width="100%" alt="Day - Rainy" /> | **Aurora Borealis** <br> <img src="https://github.com/user-attachments/assets/9591e9ef-50a6-4d67-be23-a6f51b92efd6" width="100%" alt="Night - Aurora" /> |

## Screenshots (The Complete Scene)

| Day (Light Mode) | Night (Dark Mode) |
| :---: | :---: |
| <img src="https://github.com/user-attachments/assets/df860538-703c-4cf0-8e61-135169ec3145" width="100%" alt="Dashboard Day View 1" /> | <img src="https://github.com/user-attachments/assets/78327984-0097-4cea-b19e-ef20e3e6f14a" width="100%" alt="Dashboard Night View 1" /> |
| <img src="https://github.com/user-attachments/assets/6d07c654-c791-483a-9351-ce3ec33ff083" width="100%" alt="Dashboard Day View 2" /> | <img src="https://github.com/user-attachments/assets/f6fa7d65-8777-4746-9878-b32a1960b470" width="100%" alt="Dashboard Night View 2" /> |

<details>
  <summary>About the screenshots</summary>

  These images display a complete dashboard layout. Please note that this component provides the **animated weather background and house visualization only**. The overlay buttons shown are separate elements; to replicate them, please refer to the included `paper-buttons-row-example.yml`.
</details>

## Technical Features

* **Animated Ambient Environment:** Includes wind-blown leaves, drifting fog banks, randomized lightning bolts, and sun rays with heat shimmer. The sky stays busy with airplanes, birds in various formations, shooting stars, comets, and the rare Aurora Borealis.
* **Organic Cloud Generation:** Uses a custom generator to create unique, realistic cloud shapes every time, ensuring your sky never looks repetitive.
* **Dynamic Weather Physics:** Individual particles for rain, snow, and hail with custom physics for speed, turbulence, and wobbling.
* **Real-Time Moon Rendering:** Calculates and draws the exact moon illumination and terminator line based on your sensor data.
* **Supports using your own custom image:** Personalize the card by displaying your own image on the right side. It is perfect for a transparent PNG of your home, boat, or wherever your Home Assistant is running.
* **Performance & Battery Optimized:** Automatically pauses animations when the card is hidden from view and uses debounced resizing to prevent dashboard lag.

## Installation

<details>
<summary><b>Method 1: HACS (Recommended)</b></summary>

1. Open **HACS** in Home Assistant.
2. Go to **Frontend** > **Custom repositories** (via the top-right menu).
3. Add this repository URL and select the category **Dashboard**.
4. Click **Install**.
5. When prompted, accept the option to reload the dashboard.
</details>

<details>
<summary><b>Method 2: Manual Installation</b></summary>

1. Download the `atmospheric-weather-card.js` file from the latest release.
2. Upload the file to your Home Assistant `config/www/` folder.
3. Go to **Settings** > **Dashboards** > **Three Dots Icon** > **Resources**.
4. Click **Add Resource**:
    * **URL:** `/local/atmospheric-weather-card.js`
    * **Resource Type:** JavaScript Module
5. Refresh your browser (clear cache) to load the card.
</details>

## Configuration

### Standalone Mode Example
Use this config to add a simple, beautiful weather card to any view.

```yaml
type: custom:atmospheric-weather-card
weather_entity: weather.forecast
card_style: standalone
card_height: 110
offset: 24px 0px 24px 0px
sun_moon_x_position: -55
sun_moon_y_position: 55
mode: auto
sun_entity: sun.sun
tap_action:
  action: more-info
  entity: weather.forecast

```

### Immersive Mode Example
Use this config if you want to use the card as a background, or combined with a transparent image of your home.

```yaml
type: custom:atmospheric-weather-card
weather_entity: weather.forecast_home
card_style: false   # <--- ENABLE IMMERSIVE MODE (Default)

# --- Layout ---
card_height: 200px
full_width: true    # Removes margins for full edge-to-edge effects
offset: "-50px 0px 0px 0px" # Top Right Bottom Left
sun_moon_x_position: -50
sun_moon_y_position: 40

# --- Optional: Custom Images ---
# You can display a transparent PNG of your house on top of the weather
image_scale: 100
image_alignment: bottom
day: /local/images/my-house-day.png
night: /local/images/my-house-night.png

# --- Optional: Smart Status ---
status_entity: binary_sensor.front_door
status_image_day: /local/images/house-open-day.png
status_image_night: /local/images/house-open-night.png

# --- Logic & Automation ---
mode: auto
theme_entity: input_select.theme
sun_entity: sun.sun
moon_phase_entity: sensor.moon_phase
```

## Feature Documentation

### Smart Day/Night Logic
The card uses a strict 3-layer priority system to decide between Night and Day effects.

| Priority | Name | Config Option | Logic |
| :--- | :--- | :--- | :--- |
| **1** | **Manual Mode** | `mode` | If set to `light` or `dark`, it overrides everything. |
| **2** | **Theme Entity** | `theme_entity` | Applies night visuals if state is "Dark" or "Night". |
| **3** | **Automation** | `sun_entity` | Fallback. Checks if sun is `below_horizon`. |

### Smart Text (Standalone Mode Only)
When using `card_style: true`, the card displays the temperature and location.
* **Auto-Alignment:** The card is aware of the Sun/Moon position. If the Sun is on the Left, the text automatically moves to the Right to avoid overlapping.
* **Locale Formatting:** Temperature decimals (e.g., `20.5` vs `20,5`) are automatically formatted based on your Home Assistant language settings.

### Celestial Positioning
Control where the Sun and Moon appear.
* **`sun_moon_x_position`**: Horizontal placement. Positive numbers (e.g., `50`) offset from the **Left**. Negative numbers (e.g., `-50`) offset from the **Right**.
* **`sun_moon_y_position`**: Vertical distance from the **Top**.

### Generic Status Entity
Trigger an image change if the entity is in any active state: `on`, `open`, `unlocked`, `true`, `home`, `active`.

| Category | Example Entity | Active State |
| :--- | :--- | :--- |
| **Door/Window** | `binary_sensor.front_door` | `open` |
| **Locks** | `lock.front_door` | `unlocked` |
| **Modes** | `input_boolean.party_mode` | `on` |
| **Presence** | `zone.home` | `active` |

### Layout Offset
* **Syntax:** `"Top Right Bottom Left"` (e.g., `"-50px 0px 0px 0px"`).
* **Purpose:** Use negative values to pull the weather card behind other elements.

## Custom House Image Generation

To get the "Immersive" look with your own home:

1. **Capture a Reference:** Take a photo from a corner to help the AI understand depth.
2. **Generate the Image:** Use the prompt below for a clean 3D architectural look.

> **Prompt Template:**
> Isometric view of a modern minimalist architectural model section from the outside on solid white background. [Describe your specific floors or rooms here]. Materials are matte white and light wood only. No complex textures, studio lighting, very clean, simplified shapes.

3. **Remove the Background:** Save as a transparent PNG so weather effects appear behind the house.

## Adding Buttons
To achieve the floating button look seen in the screenshots, place a `custom:paper-buttons-row` card before this card and use the `offset` feature to layer them.
