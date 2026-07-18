# ⛰️ Procedural Voxel Terrain Generator (Unity)

https://youtu.be/8eOrx_TmGOE

![C#](https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=c-sharp&logoColor=white)
![Unity](https://img.shields.io/badge/Unity-100000?style=for-the-badge&logo=unity&logoColor=white)
![Algorithms](https://img.shields.io/badge/Procedural_Generation-Algorithms-blue?style=for-the-badge)

A high-performance, procedural voxel terrain engine built in Unity. This project generates infinite, Minecraft-like worlds in real-time using advanced mathematical noise algorithms, multi-threading, and custom mesh generation techniques. 

This repository was created as an Engineering Degree Project, focusing on **architecture scalability, GPU rendering optimization**, and **advanced mathematical algorithms** for game development.

## 🚀 Key Features & Algorithms

### 1. Fractal Brownian Motion (fBm) Terrain
Instead of simple Perlin noise, the terrain relief is shaped using **fractal noise (octaves)**. By overlaying multiple layers of noise with varying frequency (Lacunarity) and amplitude (Persistence), the engine generates highly realistic mountains, hills, and plains with fine, sharp details.

### 2. Voronoi / Cellular Noise Biomes
The world is mathematically divided into distinct climate zones (biomes) using **Voronoi Diagrams**. By calculating the distance to pseudo-random control points on a grid, the engine assigns logical and sharp borders to Snowy, Grassy, and Rocky biomes without unnatural blending.

### 3. Poisson Disk Approximation (Jittered Grid)
To achieve natural-looking forests, standard random generation was rejected. Instead, vegetation uses a **Jittered Grid approach**. The chunk is divided into cells (e.g., 6x6), ensuring only one tree spawns per cell with a random offset. This guarantees perfect, organic spacing between trees, preventing them from overlapping or colliding.

### 4. Custom Vertex Ambient Occlusion (AO)
The project utilizes a custom **Voxel AO algorithm** directly baked into the 3D mesh. When constructing walls, the engine checks neighboring voxels and darkens the vertex colors in corners. A custom Shader Graph reads these vertex colors, providing photorealistic geometry depth **with zero GPU cost**.

### 5. Multi-threaded Architecture
To eliminate CPU bottlenecks and lag spikes during infinite exploration, the heavy mathematical calculations (fBm, Voronoi, Cave 3D Noise) are offloaded to background processor cores using `System.Threading.Tasks`. The Unity Main Thread is reserved solely for final mesh rendering, ensuring perfect FPS stability.

### 6. Face Culling & Procedural Meshes
No GameObjects or Prefabs are instantiated for blocks. Instead, entire 16x128x16 chunks are compiled into a single custom 3D Mesh. The **Face Culling** algorithm discards hidden faces between solid blocks, reducing the total triangle count by over 80% and dropping Draw Calls to a minimum.

---

## 🎮 How to Run the Playable Prototype

This repository contains a pre-built Windows executable. You do not need the Unity Editor to run this project.

1. Download the repository to your computer (Click **Code** -> **Download ZIP** and extract it).
2. Open the extracted folder.
3. Double-click the **`Projekt_inzynierski.exe`** file to launch the application.

### Controls
*   **W, A, S, D** - Move around
*   **Mouse** - Look around
*   **Space** - Jump

---

## 📚 References & Literature

The mathematical foundation of this project is based on established computer science literature:
*   *The Nature of Code* by Daniel Shiffman (Perlin Noise, fBm).
*   *Procedural Generation in Game Design* by Tanya Short & Tarn Adams.
*   *An Image Synthesizer (ACM SIGGRAPH)* by Ken Perlin.
*   *Meshing in a Minecraft Game* (0fps.net) - Face Culling concepts.

---
*Created as an Engineering Degree Project.*
