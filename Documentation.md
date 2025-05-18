<!-- LOGO PLACEHOLDER -->
<p align="center">
  <img src="public/images/logo.png" alt="Dreambound Logo" width="200"/>
</p>

# 🌌 Dreambound

> 🛠️ This documentation was used by our team as a starting point to learn and build with **Babylon.js**.  
> 🎮 It's now available for anyone who wants to dive into 3D web development and explore Babylon’s capabilities while following a practical game project.

---

## 📖 Table of Contents

- [🧠 Project Architecture](#-project-architecture)
- [🔦 Camera and Light Setup](#-camera-and-light-setup)
- [🌍 Scenes Overview](#-scenes-overview)
- [🎭 Animations](#-animations)
- [🧠 Physics, Collisions & Triggers](#-physics-collisions--triggers)
- [🧰 Development Tools](#-development-tools)
- [📌 About the Project](#-about-the-project)
- [🙌 Credits](#-credits)

---


# 🧠 Project Architecture

This project is structured into modular folders handling everything from meshes and animations to physics and sound.

<details>
<summary><strong>📁 Folder Structure</strong></summary>

```
/public                # Static assets served by the webserver
  ├── audio            # Sound effects and voice clips
  ├── images           # Textures, logos, sprites
  ├── models           # GLB 3D models
  └── style            # CSS

/src                   # Main source code
  ├── actions              # Lock/unlock controls
  ├── animations           # Object and character animations
  ├── cameras              # Camera setup
  ├── effects              # Visual effects and shaders
  ├── interactionsNarrator # Narrator speech and logic
  ├── level3Actions        # Cloud cannons, projectiles
  ├── lights               # Lighting setup
  ├── meshes               # Generated meshes and environments
  ├── models               # Model loading and wrappers
  ├── physics              # Collisions, gravity, triggers
  ├── scenes               # Scene organization (levels, sandbox)
  └── sounds               # Audio engine setup
```

</details>

---

# 🔦 Camera and Light Setup

## 🎥 Camera – Free Camera

We used a **FreeCamera** to allow the player full freedom of movement and look direction — essential for exploring a 3D dream world.

```js
const camera = new FreeCamera("FreeCam", new Vector3(0, 1.5, -5), scene);
camera.attachControl(canvas, true);
camera.speed = 0.3;
camera.angularSensibility = 2000;
```

### 🔧 Notes:
- `attachControl` connects the camera to mouse/keyboard input.
- `angularSensibility` controls mouse sensitivity.
- `speed` sets the player’s movement speed.

We also enabled gravity and collision detection:

```js
camera.applyGravity = true;
camera.checkCollisions = true;
camera.ellipsoid = new Vector3(0.5, 1, 0.5);
```

---

## 💡 Light – Hemispheric Light

We used a **HemisphericLight** to simulate natural ambient lighting. It provides a soft light from above and a dimmer one from below.

```js
const light = new HemisphericLight("hemiLight", new Vector3(0, 1, 0), scene);
light.intensity = 0.7;
```

- Soft lighting that simulates daylight.
- No harsh directionality — perfect for a dreamlike atmosphere.

---

# 🌍 Scenes Overview

The game is structured into **three levels** and a **sandbox**:

- **Level 1** – Introduction and basic platforming  
- **Level 2** – Interactive paths and challenges  
- **Level 3** – Cloud cannons, projectiles, final platform  
- **Sandbox** – For testing new mechanics

Each level is modular and defined in its own script in `/src/scenes`.

---

# 🎭 Animations

This project integrates Babylon.js’s animation engine to create a dynamic and immersive experience with a combination of simple and character-driven animations.

### Key Features:

- 🔁 **Continuous Rotations**  
  Objects such as decorative elements or in-game hints rotate continuously to draw attention or suggest interactivity.

- 🕴️ **Character Animations with Mixamo**  
  Characters are rigged and animated using [Mixamo](https://www.mixamo.com/), allowing them to walk, idle, or perform special actions.  
  Imported `.glb` models come with baked animations, which are triggered programmatically.

- 🕰️ **Clock and Duck Animations**  
  - The in-game clock’s hands rotate to simulate time progression.  
  - Ducks rotate on a loop to add whimsical, dreamlike motion.

- 🎞️ **Animation with FPS and Keyframes**  
  Babylon.js animations use frame-based systems where each animation is defined with keyframes.  
  - Example: A rotation animation from frame 0 to 100 with easing.  
  - FPS (Frames per second) determines how smooth the animation looks.

- 🎮 **Start/Stop Controls**  
  Custom triggers allow animations to be paused or resumed based on user interactions, proximity, or in-game events.  
  This adds interactivity and improves performance by not animating inactive objects.
---

# 🧠 Physics, Collisions & Triggers

The game uses Babylon.js’s **CannonJS physics engine** to simulate realistic physical interactions between objects and player elements.

### Physics Engine Setup:

- ⚙️ **Physics Impostors**  
  Objects are assigned physics impostors to simulate physical properties:  
  - `mass`: for weight/gravity calculations  
  - `restitution`: for bounce effects  
  - `friction`: to prevent sliding

  Example:
  ```js
  mesh.physicsImpostor = new PhysicsImpostor(mesh, PhysicsImpostor.BoxImpostor, {
    mass: 1,
    restitution: 0.2
  }, scene);
  ```

- 💥 **Collision Detection**  
  Physics-based collisions are detected using `registerOnPhysicsCollide`, enabling complex behavior like:  
  - Triggering explosions or effects  
  - Resetting the player's position  
  - Playing sounds or animations

- 🎯 **Non-physics Triggers**  
  Lightweight logic uses `intersectsMesh()` for overlap detection:  
  - Ideal for cutscenes or environmental triggers  
  - No need to simulate full physics  
  - Used for player-NPC interactions, hints, or dialogue triggers

- 🌍 **Gravity & Scaling Interactions**  
  - Player and camera are affected by gravity using `applyGravity = true`  
  - Scalable triggers change object size upon interaction for visual feedback  
  - Projectiles fired by cloud cannons collide with the player, triggering a position reset

- 💨 **Projectile System**  
  - Cloud projectiles have their own impostors and interact with both terrain and players  
  - Timed spawning and straight-line movement  
  - On impact: visual effects + camera reposition
---


# 🧰 Development Tools

| Tool       | Purpose                          |
|------------|----------------------------------|
| VS Code    | Code editing                     |
| GitLab     | Version control                  |
| Firebase   | Web hosting & deployment         |
| Blender    | 3D modeling and animations       |
| Mixamo     | Character animation generation   |

---

# 📌 About the Project

🎓 This project was developed as part of our academic journey and submitted for the **Games on Web 2025** competition.

💡 It helped us strengthen our skills in 3D web development using **Babylon.js**.

🔁 It is reusable, extendable, and serves as a foundation for future interactive 3D games on the web.

---

# 🙌 Credits

Developed by students of **[University of Upper Alsace]**  
Game design, development, and assets by **[Amine HADDAB & Gana ABDELKADER]**

---

✨ *Feel free to fork, remix, and build on this to explore Babylon.js game development!*





