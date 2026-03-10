SkySpotter

SkySpotter is a browser-based 3D flight tracking visualization tool. It consumes live ADS-B data and real-time weather APIs to render live aircraft traffic over procedurally generated representations of major global airports.

Built entirely in a single HTML file using Three.js and vanilla JavaScript.

Core Features

Live ADS-B Tracking: Fetches real-time latitude, longitude, altitude, heading, and velocity data for aircraft within a specified radius of the observation point.

Georeferenced Geometry: Real-world GPS coordinates for aircraft, runways, and terminal hubs are mathematically projected onto a localized 3D Cartesian grid at a 1:20 scale.

Real-Time Environment: Connects to local weather data to accurately simulate current conditions, including day/night cycles, cloud cover, fog, rain, snow, and thunderstorms.

Procedural Spatial Audio: Generates dynamic wind, storm, and jet engine noise using the Web Audio API. Audio is spatially panned and uses distance-based lowpass filtering to simulate atmospheric muffling. No external audio assets are used.

Dynamic Scenery: Runways, edge lights, and terminal blocks are generated procedurally based on hardcoded real-world threshold coordinates to prevent intersection and ensure aircraft align with the tarmac.

Observation Stances: View the airspace from distinct heights (0.3m, 1.0m, 100m) to observe traffic from ground level or an elevated radar perspective.

Data Sources

Flight Data: OpenSky Network API

Weather & Sunrise/Sunset Data: Open-Meteo API

Supported Locations

The camera is anchored to specific geographic observation points near the following airports:

Singapore (SIN): Changi Beach

New York (JFK): TWA Hotel (Central Terminal Area)

London (LHR): Myrtle Avenue

Tokyo (HND): Jonanjima Seaside Park

Dubai (DXB): Al Garhoud Park

Technical Architecture

Rendering: WebGL via Three.js. Relies heavily on InstancedMesh for ground clutter (grass, trees, buildings) to maintain high frame rates.

Scale: The world operates on a constant SCALE = 0.05. One WebGL unit equals 20 real-world meters.

Illusion of Depth: The skybox, stars, and distant procedural clouds are rendered on a miniaturized sphere tethered to the camera position with depthWrite: false and a negative renderOrder. This prevents Z-fighting and hardware clipping while maintaining infinite visual parallax.

Zero Dependencies (Assets): The project does not load any external 3D models, textures, or audio files. All assets are procedurally generated via canvas elements, geometry primitives, custom shaders, and audio oscillators.

Running Locally

Because the project is entirely self-contained, no build step or package manager is required.

Clone the repository.

Open SkySpotter.html in any modern web browser.

Note: Strict browser security settings or ad-blockers may occasionally block the external API calls to OpenSky or Open-Meteo. The app will fallback to simulated traffic if the connection drops.

Controls

Click & Drag: Pan camera (yaw/pitch).

HUD Toggles: Enable/disable flight paths and aircraft identification tags.

Stance Buttons: Change camera elevation.

Debug Mode: Press Ctrl + Cmd + R (Mac) or Ctrl + Windows + R (PC) to cycle through weather states (Clear -> Rain -> Thunderstorm) regardless of actual local weather.
