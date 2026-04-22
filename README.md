# piano-learning-application
# 🎹 Piano Practice Dashboard: Flow State Edition

A gamified, interactive piano learning dashboard built entirely with Vanilla JavaScript, HTML, and CSS. This application connects directly to your digital piano via the Web MIDI API, allowing you to practice scales with real-time feedback, fingering guides, and performance analytics. 

Designed to induce a "flow state," the app features an auto-randomizing "Surprise Mode" and an inactivity timeout to keep your fingers moving and your mind engaged.

## ✨ Features

* **🔌 Web MIDI Integration:** Plug in any MIDI-compatible keyboard. The app instantly recognizes your inputs, velocities, and note releases.
* **🖐️ Dynamic Fingering Guides:** Displays exact left-hand (LH) and right-hand (RH) fingering numbers for every major and minor scale across all 12 keys. The visual hands highlight the specific finger you should be using in real-time.
* **🎲 Surprise Mode (Flow State):** Toggle "Surprise Mode" to auto-generate random scales (Mix, Major-only, or Minor-only). When you complete a scale, the next one generates instantly. If you pause for more than 4 seconds, the system nudges you forward with a new challenge.
* **🎯 Target Highlighting:** The virtual keyboard visually guides you. It highlights your current target note in green, previews the next note in yellow, and flashes red if you make a mistake.
* **⏱️ Real-time Analytics:** Tracks your time-to-completion and calculates your accuracy percentage based on your misstrikes.
* **🔊 Audio Demonstration:** Don't have a MIDI keyboard plugged in? Click "Play Demo" to hear the scale synthesized directly in your browser using the Web Audio API.

## 🛠️ Technologies Used

* **Frontend:** HTML5, CSS3, Vanilla JavaScript
* **Hardware API:** Web MIDI API (`navigator.requestMIDIAccess`)
* **Audio API:** Web Audio API (`AudioContext`) for built-in triangle wave synthesis.

## 🚀 Getting Started

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/Fourier-Laplace-0/piano-learning-application.git](https://github.com/Fourier-Laplace-0/piano-learning-application.git)
    ```
2.  **Open the application:**
    Because this app uses the Web MIDI API, **it must be served over HTTPS or `localhost`** (browser security requirement). 
    
    Serve it via a simple local server:
    ```bash
    # Using Python
    python -m http.server 8000
    
    # Or using Node.js (http-server)
    npx http-server
    ```
    Then navigate to `http://localhost:8000` in a Chrome, Edge, or Opera browser (Safari/Firefox require manual MIDI flags/plugins).

3.  **Connect your Keyboard:**
    Plug in your MIDI keyboard via USB. Refresh the page, and the status bar should turn green and display your device's name.

## 🌐 Deployment
Because this application is purely client-side with no backend database, it is highly portable. It is optimized for rapid deployment to edge networks like Cloudflare Workers or GitHub Pages, making it incredibly easy to host under a custom domain or specific subdomains.

## 🧠 How it Works

1. **Music Theory Engine:** The app uses an internal matrix of intervals (`[0, 2, 4, 5, 7, 9, 11]` for Major) and a comprehensive dictionary of standard piano fingerings to calculate the exact path up and down the keyboard for any root note.
2. **Event Listeners:** The `onMIDISuccess` callback hooks into your keyboard. It listens for `144` (Note On) and `128` (Note Off) commands, comparing your physical key presses against the `currentScaleSequence` array.
3. **State Management:** Global variables track your `currentStep`, updating the DOM UI (highlighting the next key and lighting up the correct finger on the visual hands) on every correct, sequential press.
