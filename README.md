<p align="center">
<img src="https://ariss-ea.org/wp-content/uploads/2024/08/logo_color-2048x904.png" alt="Logo ARISS-EA" width="300"/>
</p>

# ARISS-EA SSTV Mosaic Generator

A lightweight, WordPress-friendly HTML/JavaScript/CSS widget for creating personalized SSTV mosaics from ARISS SSTV events. Users can upload up to 12 SSTV frames plus an optional diploma image, pick from several backgrounds (or upload their own), and download a single combined JPEG featuring the ISS Expedition logo logo, titles, personal info, image grid, and diploma.

# Authors

* Alejandro Romero (University of Castilla-La Mancha, Spain)

AI-assisted programming tools were used throughout the development of this project to improve productivity.

## Features

- **Upload & Preview** up to 12 SSTV images (640×496 or matching aspect ratio)  
- **Optional Diploma** slot with remove functionality  
- **Background Selection**  
  - International Space Station  
  - ARISS Antenna (Columbus Module)  
  - Pillars of Creation (JWST)  
  - High-Contrast White & Black  
  - Custom upload (with semi-transparent overlay)  

## Demo

Try it out at [ARISS-EA webpage](https://ariss-ea.org/sstv-mosaic)

## Installation

1. Change the links used for backgrounds that point to the ARISS-EA website. 
2. **Copy** the contents of `index.html` into a WordPress **Custom HTML** widget (using the “Custom HTML” block).  
3. **Ensure** the Inter font is available (you can enqueue it via your theme or add a `<link>` to Google Fonts).  
4. **Publish** your page—your SSTV Mosaic Generator is ready to use!

## Usage

1. Enter your **Name** and **Grid Square** (callsign is optional).  
2. Click any “No image” slot to upload SSTV frames; use the red **Remove** button to clear a slot.  
3. (Optional) Upload the official **Diploma**.  
4. Select a **Background**, or upload your own for a custom backdrop.  
5. Hit **Save Mosaic as JPG**—the widget validates inputs, combines everything on a hidden `<canvas>`, and triggers a download of your mosaic.

## Development

This project is built with plain HTML, CSS, and vanilla JavaScript—no build tools or external dependencies required.  
Feel free to explore the code, tweak the styles or behavior, and experiment directly in your favorite editor. All of the functionality (image uploads, canvas rendering, background selection, etc.) lives in a single self-contained snippet that you can drop into any WordPress Custom HTML block or similar.

## Contributing

We welcome feedback, improvements, and new ideas! If you’d like to suggest enhancements or fix bugs, just open a pull request on this repository. We review all submissions and will be happy to merge any changes that help make the SSTV Mosaic Generator even better.  

