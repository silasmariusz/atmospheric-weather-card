# Atmospheric Weather Card


> **AI-DISCLAIMER:**
> This card was created with the help of AI.

| Night View | Day View |
| :---: | :---: |
| <img src="https://github.com/user-attachments/assets/878c8e41-04ed-4cf4-a09d-2c079a0f427a" width="400"> | <img src="https://github.com/user-attachments/assets/2a58f714-74ba-426e-8492-afdc541053e1" width="400"> |



> **Info about the screenshots:** This shows a "finished" dashboard example. This card provides the **animated weather background and house image only**. The buttons you see floating on top are *not included*—they are separate cards (e.g., `paper-buttons-row`) that I placed over the weather card.

## Technical Features
* **Triple-Layer Canvas Engine:** Uses dedicated background, middle, and foreground layers to create a sense of depth between weather effects and your home image.
* **Organic Cloud Generation:** Uses a custom generator to create unique, non-repeating cloud shapes including cumulus, stratus, and cirrus varieties.
* **Dynamic Weather Physics:** Individual particles for rain, snow, and hail with custom physics for speed, turbulence, and wobbling.
* **Ambient Environment:** Includes wind-blown leaves, drifting fog banks, randomized lightning bolts, airplanes, shooting stars and rare aurora borealis effects.
* **Real-Time Moon Rendering:** Calculates and draws the exact moon illumination and terminator line based on your sensor data.
* **Smart Battery Management:** Automatically pauses animations when the card is hidden from view and uses debounced resizing to prevent dashboard lag.

## Performance
This card is optimized to run smoothly on standard tablets and wall panels. Because HTML Canvas animations can be demanding on hardware, the visual effects and frame rate are intentionally toned down to prevent your Home Assistant dashboard from lagging or becoming unresponsive.

## Installation

### Method 1: HACS (Recommended)
1.  Open **HACS** in Home Assistant.
2.  Go to **Frontend** > **Custom repositories** (via the top-right menu).
3.  Add this repository URL and select the category **Dashboard**.
4.  Click **Install**.
5.  When prompted, accept the option to reload the dashboard.

### Method 2: Manual Installation
1.  Download the `atmospheric-weather-card.js` file from the latest release.
2.  Upload the file to your Home Assistant `config/www/` folder.
3.  Go to **Settings** > **Dashboards** > **Three Dots Icon** > **Resources**.
4.  Click **Add Resource**:
    * **URL:** `/local/atmospheric-weather-card.js`
    * **Resource Type:** JavaScript Module
5.  Refresh your browser (clear cache) to load the card.

## Configuration

### Basic Usage
The only strict requirement is a weather entity.

```yaml
type: custom:atmospheric-weather-card
weather_entity: weather.forecast_home
```

### Full Configuration (Recommended)
To get the full effect with your own home image and moon phases:

```yaml
type: custom:atmospheric-weather-card
weather_entity: weather.forecast_home
# Optional: Full width mode. This feature dynamically detects your dashboard's CSS variables and applies negative margins so the card uses the full display width.
full_width: false
# Optional: Shows accurate moon phases on clear nights
moon_phase_entity: sensor.moon_phase
# Optional: Manual Dark/Light Mode Toggle
theme_entity: input_select.theme
# Optional: Your custom images (transparent PNGs recommended)
day: /local/images/my-house-day.png
night: /local/images/my-house-night.png
# Optional: Change house image based on a door sensor
door_entity: binary_sensor.front_door
# Optional: Alternate images when door is open
door_open_day: /local/images/house-open-day.png
door_open_night: /local/images/house-open-night.png
```

### How to use the Dark/Light Mode Toggle
The card can automatically switch its visuals (like stars vs sun) based on an Input Select helper.

1.  Go to Settings > Devices & Services > Helpers.
2.  Create a new **Dropdown (Input Select)**.
3.  Name it (e.g., "Theme").
4.  Add two options: **dark** and **light**.
5.  Add the entity ID (e.g., `input_select.theme`) to your card configuration as shown above.

When this helper is set to "dark", the card will render night visuals (stars, dark clouds) regardless of the actual sun position.

## Custom House Image Generation

You can create a personalized 3D-style image for this card using AI image generators (like Midjourney or DALL-E 3) without needing 3D modeling skills.

**1. Capture a Reference:** Take a clear photo of your house or the specific area you want to display. Aim for a wide shot that shows the overall layout. Taking the photo from a corner usually helps the AI understand the perspective and depth better.

**2. Generate the Image:** Use a prompt that focuses on a "clean model" aesthetic. You can use the template below, adjusting the description to match your specific home layout.

**Prompt Template:**
Isometric view of a modern minimalist architectural model section from the outside. [Describe your specific floors or rooms here]. Materials are matte white and light wood only. No complex textures, studio lighting, very clean, simplified shapes.


## Troubleshooting
* **Card is blank?** Make sure you have refreshed your browser cache.
* **Visuals look pixelated?** This is intentional for performance. I want to focus on stability first and increase the visuals gradually.
* **Dark Mode:** This card looks best when your dashboard theme is set to **Dark Mode**, as the particle effects (stars, rain) stand out better.
