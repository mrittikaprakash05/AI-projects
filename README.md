

✨ Interactive 3D Particle System with Hand Tracking


A real-time, browser-based 3D simulation where a cloud of 8,000 particles reacts physically to your hand movements using your webcam. Built with Three.js for rendering and Google MediaPipe for computer vision.

🎮 Features

Real-Time Hand Tracking: Detects hand position instantly using the webcam (no dedicated hardware required).

Physics-Based Interaction: Particles react to the presence of the hand using repulsion forces and vector mathematics.

High Performance: Renders 8,000+ particles simultaneously using BufferGeometry and typed arrays (Float32Array) for 60FPS performance.

3D Depth: Maps 2D video coordinates into a 3D environment for immersive depth interaction.

🛠️ Tech Stack

Three.js: For high-performance WebGL 3D rendering.

MediaPipe Hands: For machine-learning-based hand tracking directly in the browser.

HTML5 / JavaScript (ES6): Core logic.

📦 How to Run Locally

Because this project accesses the webcam, browser security policies require it to run on a secure context (HTTPS) or localhost. It will not work if you simply double-click the HTML file.

Option 1: VS Code 

Clone or download this repository.

Open the folder in VS Code.

Install the "Live Server" extension.

Right-click index.html and select "Open with Live Server".

Option 2: Python Simple Server

If you have Python installed, you can run a server from the terminal:

code
Bash
download
content_copy
expand_less
# Go to the folder
cd path/to/folder

# Start server
python -m http.server 8000

Then open your browser to http://localhost:8000.

🧠 How it Works
1. The Particle System

The cloud is built using a BufferGeometry. Unlike standard objects, we store position and color data in Typed Arrays. This allows the GPU to handle thousands of points efficiently without lagging the CPU.

2. The Physics Engine

In every animation frame, the code calculates the distance between every single particle and the user's hand position using the distance formula:

d = ((x2-x1)^2 + ( y2-y1)^2 + (z2-z1)^2)^1/2
	​


If Hand is Close: A repulsion vector is calculated to push the particle away.

If Hand is Far: The particle slowly interpolates (drifts) back to its original "home" position.

3. Computer Vision

We use MediaPipe Hands to detect landmarks on the user's hand. We specifically track Landmark 8 (Index Finger Tip). The 2D coordinates (X, Y) from the video feed are normalized and mapped to the 3D world coordinates of the Three.js scene.

🎨 Customization

You can tweak the physics and visuals by editing the constants at the top of the script:

code
JavaScript
download
content_copy
expand_less
const PARTICLE_COUNT = 8000;   // Number of particles (Lower this if lagging)
const REACTION_RADIUS = 30;    // How big the "push" area is
const REACTION_SPEED = 0.5;    // How fast particles fly away
const RETURN_SPEED = 0.05;     // How fast they float back
⚠️ Troubleshooting

"Loading..." stays forever: Check your browser console (F12). If you see "Permission denied," you must allow camera access in your browser settings.

Black Screen: Ensure you are running on a local server (http://localhost or https://), not file://.

📄 License

This project is open source and available under the MIT License.
