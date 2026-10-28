<p align="center">
<img src="https://ariss-ea.org/wp-content/uploads/2024/08/logo_color-2048x904.png" alt="Logo ARISS-EA" width="300"/>
</p>

# ARISS-EA SSTV Mosaic Generator

A lightweight, WordPress-friendly HTML/JavaScript/CSS widget for creating personalized mosaics from ARISS SSTV events. Users add the SSTV frames they receive from the International Space Station, optionally include their ARISS diploma, choose a background and download a single JPEG with the event title, expedition and ARISS logos, their personal details, the image grid and the diploma.

Version 2.1 also predicts the next ISS passes over the user's station, generates SWL cards for individual frames and exports a vertical version for social media stories.

# Authors

* Alejandro Romero (University of Castilla-La Mancha, Spain)

AI-assisted programming tools were used throughout the development of this project to improve productivity.

## Table of Contents

* [Features](#features)
* [Demo](#demo)
* [Files](#files)
* [Installation](#installation)
* [Event Configuration](#event-configuration)
* [Usage](#usage)
* [Privacy](#privacy)
* [Decomposer](#decomposer)
* [Development](#development)
* [Contributing](#contributing)

## Features

* **6 or 12 image mosaics** in **Robot36** (320x240) or **PD120** (640x496). The default mode and number of images are set for each event and can be changed in **Settings**.
* **Several ways to add frames:**

    * Click an empty slot.
    * Use **Add images** to select several files at once.
    * Drag and drop files onto the page or onto a specific slot.
    * Paste an image from the clipboard (Ctrl/Cmd+V).

* **Frame details:** tap any frame to see it larger, adjust its reception time (UTC), move it to another slot, replace it or remove it. Frames can also be reordered by dragging one onto another.
* **Reception time:** taken from the file date and editable per frame. It can optionally be shown on each frame in the mosaic.
* **"Complete set" seal**, shown when every slot has a frame.
* **Optional diploma** slot for the official ARISS SSTV certificate.
* **Backgrounds:**

    * International Space Station
    * ARISS Antenna on the Columbus Module
    * Pillars of Creation (JWST)
    * High contrast (white or black)
    * Custom upload

* **Live preview** that shows exactly what the exported mosaic will look like.
* **Export options:**

    * **Save Mosaic as JPG** for a full-resolution mosaic.
    * **Story format (9:16)** for a 1080x1920 image for Instagram, TikTok or WhatsApp stories.
    * **SWL card** for a single received frame.
    * **Share** through the system share sheet on supported phones.

* **ISS pass prediction:** after entering a Grid Square, the widget shows the next ISS passes over the station, a countdown, maximum elevation, duration, a sky track of the selected pass and the event downlink frequency.
* **Event banner** that shows whether the SSTV event is about to start or currently active.
* **Local saving:** name, images, reception times, background, diploma and settings persist across visits. It can be turned off in **Settings**, and **Clear all** removes everything that was saved.
* **Native frame resolution:** frames are stored at the native size of the SSTV mode, so the [Decomposer](#decomposer) can extract them again from a finished mosaic.

## Demo

Try it out at the [ARISS-EA webpage](https://ariss-ea.org/sstv-mosaic).

## Files

| File | Description |
| --- | --- |
| `index.html` | SSTV Mosaic Generator (v2.1). |
| `Decomposer.html` | Companion tool that extracts the frames and diploma from a mosaic. |

## Installation

1. Edit the [event configuration](#event-configuration) at the top of the script in `index.html`.
2. If you host the widget outside ariss-ea.org, replace the links to the background images and logos, which point to the ARISS-EA website.
3. Copy the contents of `index.html` into a WordPress **Custom HTML** block.
4. Make sure the Inter font is available, either through your theme or by adding a `<link>` to Google Fonts. Arial is used as a fallback.
5. Publish the page.

All CSS is scoped to `#ariss-sstv-mosaic`, so the widget does not affect the rest of the site.

**WordPress note:** do not write a bare less-than sign inside the script. WordPress may treat it as the start of an HTML tag and turn the following `&&` into `&#038;&#038;`, which breaks the script. Write comparisons the other way round (`b > a`).

## Event Configuration

Each SSTV series is configured with a few constants at the top of the script:

| Constant | Description |
| --- | --- |
| `EVENT_TITLE` | Event title, for example `ARISS SSTV Series 34`. It is shown on the page and drawn on the mosaic. |
| `EVENT_SUBTITLE` | Event theme, for example `ARISS Hardware`. |
| `EXPEDITION_LOGO_URL` | Logo of the current ISS expedition. |
| `ARISS_LOGO_URL` | ARISS logo drawn on the mosaic. |
| `DEFAULT_MOSAIC_MODE` | Default number of images: `6` or `12`. |
| `DEFAULT_SSTV_FORMAT` | Default SSTV mode: `'robot36'` or `'pd120'`. |
| `EVENT_START` / `EVENT_END` | Event window in UTC (ISO 8601). Set to `null` to hide the event banner. |
| `DOWNLINK` | Downlink frequency shown with the ISS passes, for example `437.550 MHz FM`. |
| `SCHEDULE` | Transmission schedule shown next to the frequency. Leave empty to hide it. |

The title and subtitle are defined only here. Browser translation can change the page text, but never what is drawn on the mosaic.

### ISS orbital data

Pass prediction uses [satellite.js](https://github.com/shashwatak/satellite-js), loaded from cdnjs, and the current ISS TLE. The widget first requests a cached copy from `/tle-cache/tle.json` on ariss-ea.org and falls back to the public [Where the ISS at?](https://wheretheiss.at/) API. If you host the widget on another site, either serve your own TLE cache at that path or rely on the fallback.

## Usage

1. Enter your **Name** and **Grid Square**. The callsign is optional.
2. Check **When can I receive the ISS?** to see the next passes over your station and the downlink frequency.
3. Add the SSTV frames you receive by clicking a slot, using **Add images**, dragging and dropping, or pasting them.
4. Click a frame to see it larger, adjust its reception time, move it or create an **SWL card**.
5. Optionally add the official **Diploma** and choose a **Background**.
6. Click **Save Mosaic as JPG**, or **Story format (9:16)** for social media.

### Official ARISS certificate

The generator does not send any images to ARISS. To get the official certificate, upload your images to the [ARISS SSTV Gallery](https://ariss-usa.org/ARISS_SSTV/). Once you receive it, you can add it to your mosaic as the diploma.

## Privacy

Everything is processed in the browser. Images and personal details are only stored in the browser's local storage when local saving is enabled, and they are never uploaded. The ISS pass prediction is also computed in the browser.

The widget only makes network requests to load its images and logos, the satellite.js library and the ISS orbital data.

## Decomposer

`Decomposer.html` is a companion tool that does the reverse process: it takes a finished mosaic and extracts the individual SSTV frames and the diploma.

* Automatically detects 6 or 12 image mosaics, in Robot36 or PD120, with or without diploma.
* Supports mosaics created with older versions of the generator.
* Download each frame individually, or everything at once as a ZIP file.

It is installed the same way as the generator, in a WordPress **Custom HTML** block. Its CSS is scoped to `#ariss-sstv-decomposer`.

## Development

This project is built with plain HTML, CSS and vanilla JavaScript, with no build tools. Each tool is a single self-contained snippet that can be dropped into a WordPress Custom HTML block or any web page. The only external libraries are loaded from cdnjs: satellite.js in the generator, and JSZip and FileSaver.js in the Decomposer.

## Contributing

We welcome feedback, improvements and new ideas! If you would like to suggest enhancements or fix bugs, open an issue or a pull request on this repository, or contact us at info@ariss-ea.org.
