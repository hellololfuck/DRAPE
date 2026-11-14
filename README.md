# DRAPE

**A tiny 3D cloth-draping sandbox for Windows.**

Drop a simulated piece of fabric over a statue, a ball, a cube, a cone, a can, or a donut. Turn the mesh density from a single polygon all the way up to 100,000 polygons. Change the cloth size, the drop height, the fall speed, the colors, and the scene lighting, then drop it again and watch a different result.

No installer. No account. No internet connection. Just an `.exe` and a cloth.

[**Download the latest build**](./Drape.exe?raw=true) · [Quick start](#quick-start) · [Controls](#controls) · [Troubleshooting](#troubleshooting)

![Platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-0078D6?style=flat-square)
![Runtime](https://img.shields.io/badge/runtime-Electron%2031-47848F?style=flat-square)
![Renderer](https://img.shields.io/badge/renderer-three.js%20r128-000000?style=flat-square)
![Status](https://img.shields.io/badge/status-playable-success?style=flat-square)

---

## Table of contents

- [What is Drape?](#what-is-drape)
- [Quick start](#quick-start)
- [Your first 30 seconds](#your-first-30-seconds)
- [Controls](#controls)
- [The control panel](#the-control-panel)
- [Shapes](#shapes)
- [Themes](#themes)
- [The polygon ladder](#the-polygon-ladder)
- [Things to try](#things-to-try)
- [How the cloth works](#how-the-cloth-works)
- [Performance guide](#performance-guide)
- [System requirements](#system-requirements)
- [Troubleshooting](#troubleshooting)
- [Privacy](#privacy)
- [What is in this repository](#what-is-in-this-repository)
- [Technical notes](#technical-notes)
- [FAQ](#faq)
- [Credits](#credits)
- [License](#license)

---

## What is Drape?

Drape is a small real-time cloth simulation presented as a desktop toy. Each drop creates a square sheet of fabric above an object. Gravity pulls the sheet down, distance constraints keep the fabric from stretching, and collision constraints stop it from passing through the object underneath. The result is a soft, slightly unpredictable drape that settles into folds, ridges, and overhangs.

There is no score, no timer, and no fail state. Drape is something to poke at: change one slider, press **Drop cloth**, and see what happens. You can use it as a stress test for your GPU, a quick physics demo, or just a few minutes of watching fabric fall.

The whole experience is deliberately small:

- One object on screen at a time
- One cloth at a time
- A single portable Windows executable
- No menus beyond the control panel
- No saved data, profiles, or online services

---

## Quick start

1. Download **[Drape.exe](./Drape.exe?raw=true)**.
2. Put it anywhere you like, such as your Desktop or a games folder.
3. Double-click **Drape.exe**.
4. If Windows shows a SmartScreen warning, click **More info**, then **Run anyway**.
5. Drag the scene to rotate the camera. Press **Drop cloth** to throw a new sheet.

That is the whole installation process. The executable is portable: it does not need an installer, an administrator account, or a separate runtime.

> **Heads-up:** The build is not code-signed, so Windows may warn you the first time you run it. This is normal for small independent Windows apps. Only run the copy you downloaded from this repository.

---

## Your first 30 seconds

If you just want to see the simulation do something interesting:

1. Leave the shape on **Statue**.
2. Leave **Polygons** at the default value.
3. Press **Drop cloth**.
4. Wait a few seconds while the fabric falls and settles.
5. Drag left or right across the scene to look at the folds from another angle.
6. Move the **Cloth size** slider a little and press **Drop cloth** again.

Every drop is slightly different because the cloth starts with a small random rotation and tilt. Pressing **Drop cloth** twice will not produce an identical result.

For a hands-off demonstration, press **Play 1 → 25000**. Drape will step through a series of polygon counts on its own and re-drop the cloth at each one.

---

## Controls

| Action | How |
| --- | --- |
| Rotate the camera | Drag left or right in the 3D view |
| Drop a new cloth | Click **Drop cloth**, or change the shape, polygon count, object size, or cloth settings to rebuild automatically |
| Change the object | Click one of the shape buttons: **Statue**, **Ball**, **Cube**, **Cone**, **Can**, **Donut** |
| Change mesh density | Use the **Polygons** number box or the slider beside it |
| Run the automatic showcase | Click **Play 1 → 25000** |
| Stop the automatic showcase | Press **Drop cloth**, change the shape, polygon count, object size, or cloth settings, or press **Play 1 → 25000** again |
| Toggle a wireframe view | Tick **Wireframe** |
| Change the scene style | Use the **Colors** theme drop-down: **Studio** or **Candy** |

There are no keyboard shortcuts and no mouse-wheel zoom in this version. The camera orbits horizontally only, which keeps the object centered and the cloth in view.

The game window can be resized freely. The 3D view and control panel reflow for narrow or wide windows. On a narrow window the panel moves below the view; on a wider window it sits on the right.

---

## The control panel

Every control rebuilds or updates the simulation immediately. You do not need to restart the app.

### Polygons

**Range:** 1 to 100,000

This is the approximate number of triangles in the cloth. The simulation uses a square grid, so the actual count is rounded to the nearest square number. For example, asking for 1,500 polygons gives a 39 × 39 grid, which is 1,521 polygons. The large number above the scene shows the real count that is currently in use.

The slider is logarithmic: small values get a lot of fine control, while the upper end moves in larger jumps. That makes it practical to go from a single triangle to tens of thousands of triangles with one control.

Higher polygon counts create finer folds and more detailed contact with the object, but they also cost more CPU and GPU time. See the [performance guide](#performance-guide).

### Shape buttons

The six buttons above the sliders choose the object the cloth falls onto:

- **Statue** — a stylized bust on a plinth, with a head, shoulders, and a small topknot
- **Ball** — a sphere
- **Cube** - a box
- **Cone** — a cone pointing upward
- **Can** — a short cylinder
- **Donut** — a torus lying flat

Selecting a new shape clears the old object, rebuilds the new one, and drops a fresh cloth.

### Size

**Range:** 0.25 to 0.80, default 0.45

Scales the object underneath the cloth. A larger object creates a broader contact area and pushes the fabric outward. The statue also scales its plinth and head with this value.

### Cloth size

**Range:** 1.6 to 4.0, default 2.6

Sets the width and depth of the square cloth before it falls. A small cloth may barely cover the object; a large cloth will pool around the base and may hang over the edges.

### Drop offset

**Range:** -0.8 to +0.8, default 0

Shifts the starting position of the cloth horizontally. Use it to make the cloth land off-center, slide down one side, or leave part of the object exposed.

### Speed

**Range:** 0.3 to 3.0, default 1.4

Controls how quickly the simulation runs. Lower values give a slow, floaty drop that is easier to watch. Higher values make the cloth fall and settle faster. This changes the motion, not the physical size of the cloth.

### Stick

**Default:** on

For the non-statue shapes, **Stick** adds a thin vertical support pole and raises the object to the height set by the slider beside it. The cloth can catch on the pole and hang from it instead of falling straight to the ground. This is a quick way to create a tent-like or curtain-like drape.

**Range of the stick height slider:** 1.0 to 2.2, default 1.7

The stick is ignored when the **Statue** shape is selected, because the statue already has its own plinth and support geometry.

### Colors

Two color pickers and a theme menu:

- The left color picker changes the object material.
- The right color picker changes the cloth material.
- The drop-down switches between the **Studio** and **Candy** themes.

Changing the theme also resets both colors to that theme's defaults. You can then customize them again with the pickers.

### Wireframe

Shows the cloth as a mesh of lines instead of a solid surface. This is useful for seeing how the grid deforms and where the constraints are pulling. It is also a good way to inspect the simulation at high polygon counts without the surface shading hiding the structure.

### Drop cloth

Rebuilds the cloth above the current object and starts the simulation again. The new sheet gets a small random rotation and tilt, so repeated drops are never exactly the same.

### Play 1 → 25000

Starts an automatic demo. Drape steps through the following polygon targets, spending about 4.5 seconds at each one:

`1 → 4 → 9 → 16 → 24 → 60 → 100 → 200 → 400 → 700 → 1,500 → 3,000 → 6,000 → 12,500 → 25,000`

Each step updates the polygon count and drops a fresh cloth. The full sequence takes a little over a minute. Changing a scene-rebuilding control, such as the shape, polygon count, object size, cloth size, drop offset, or stick, stops the sequence. Pressing **Play 1 → 25000** again starts it over.

The button is a showcase, not a scored mode. It is there to let you watch the same scene at every scale from a single triangle to a fairly dense sheet.

---

## Shapes

### Statue

The default shape is a simple bust: a plinth, a torso/head mass, a neck, and a small rounded topknot. It is built from several primitives rather than a detailed sculpt, which keeps collision inexpensive and makes the cloth catch on the head and shoulders in readable ways.

The statue is the best shape for classic draping: the cloth falls over a rounded head, slides down the chest, and pools around the base.

### Ball

A sphere with a smooth collision surface. Drapes tend to form radial folds and a clean skirt around the equator. A large cloth over a small ball produces deep, even pleats.

### Cube

A box. The cloth bridges across the top, folds over the edges, and hangs down the sides. Good for testing how the simulation handles flat faces and sharp direction changes.

### Cone

A cone with a pointed top. The cloth usually slides off one side unless the **Stick** support catches it. Try a large cloth and a low drop offset for a cape-like result.

### Can

A short cylinder. The cloth wraps around the curved side and often leaves a visible seam or overlap where the two sides meet.

### Donut

A torus lying flat. The hole in the middle is the interesting part: with a large enough cloth, the fabric can bridge the hole or sink into it depending on the drop.

---

## Themes

### Studio

A dark, neutral backdrop with a warm key light, a cool fill light, and a soft spot light. The object defaults to a warm bronze color and the cloth to a muted tan. This theme is designed to make shadows and folds easy to see.

### Candy

A bright lavender backdrop with colorful scattered circles. The lights are flatter and more even, the object defaults to pink, and the cloth defaults to a warm peach. This theme is more playful and makes the cloth read as a solid shape rather than a shaded sculpture.

Both themes are generated in the app. There are no external image assets to load, which is part of why the build is self-contained.

---

## The polygon ladder

The polygon control is the main dial for both visual detail and performance. Here is what the approximate counts feel like in practice:

| Target | Grid | Actual polygons | What to expect |
| ---: | ---: | ---: | --- |
| 1 | 1 × 1 | 1 | A single flat triangle. Useful for seeing the raw simulation. |
| 16 | 4 × 4 | 16 | A coarse sheet that folds in big, angular steps. |
| 100 | 10 × 10 | 100 | Low-poly cloth; folds are chunky but readable. |
| 400 | 20 × 20 | 400 | A good balance for older laptops. |
| 1,500 | 39 × 39 | 1,521 | The default look: enough detail for soft folds. |
| 6,000 | 77 × 77 | 5,929 | Smooth folds and more convincing contact shadows. |
| 12,500 | 112 × 112 | 12,544 | Dense cloth; a dedicated GPU is helpful. |
| 25,000 | 158 × 158 | 24,964 | High detail. Expect a noticeable load on integrated graphics. |
| 100,000 | 316 × 316 | 99,856 | Maximum density. Best on a strong desktop GPU. |

Because the cloth is square, the actual count is always a square number. The number box accepts any value in the range, but the simulator rounds the grid size to the nearest whole cell count.

At very high densities, Drape reduces some of the most expensive collision work to keep the interaction responsive. The cloth still collides with the object, but fine self-collision is limited to moderate grid sizes. That trade-off is deliberate: it keeps the top of the range usable instead of turning every drop into a slideshow.

---

## Things to try

- **The classic drape:** Statue, default polygon count, cloth size around 2.6, speed 1.4. Press **Drop cloth** and watch it settle.
- **The ghost:** Statue, large cloth, drop offset near -0.8, wireframe on. The offset makes the sheet slide off one shoulder.
- **The mushroom:** Ball, stick on with a high stick height, cloth size near 4. A large sheet caught on the pole can form a wide canopy.
- **The ring:** Donut, cloth size small enough to fall through the hole, speed low. Watch how the fabric interacts with the inner edge.
- **The stress test:** Cube, 100,000 polygons, speed 1.0. Rotate the camera while it falls and watch the frame rate.
- **The candy cape:** Cone, Candy theme, large cloth, drop offset positive. The bright palette makes the folds easier to see from a distance.
- **The single triangle:** Set polygons to 1. It is less a cloth and more a flying piece of paper, but it shows the simulation's basic behavior with no constraints to hide behind.
- **The time-lapse:** Start **Play 1 → 25000** and watch the same scene gain detail as the grid resolution climbs.

---

## How the cloth works

Drape uses a real-time particle-and-constraint cloth model, rendered with three.js.

### Particles

The cloth is a grid of points. Each point stores a position and an implied previous position. The simulation advances in small steps: gravity pulls the points downward, and a damping factor gradually removes velocity. This is a Verlet-style integrator, which is simple, stable, and cheap for a grid of this size.

### Constraints

Neighboring points are linked by distance constraints. After each integration step, the solver visits the links and pulls the endpoints back toward their rest length. Multiple solver iterations make the sheet stiffer; fewer iterations let it stretch and wobble more.

At lower grid resolutions, Drape also adds longer-range links across two cells. These help a coarse sheet behave more like fabric instead of a loose net.

### Collision

The object under the cloth is represented by a mathematical collision function rather than a triangle mesh. Each shape has its own signed-distance-style test:

- Sphere and torus use radial distance
- Cube uses an axis-aligned box distance
- Cone uses a projected conical distance
- Can uses a cylinder distance
- Statue combines box, ellipsoid, and sphere-like pieces
- The stick adds a thin vertical cylinder constraint

When a cloth point ends up inside the object, the solver pushes it back to the nearest surface and removes the part of its velocity that points into the object. That is what makes the fabric slide, catch, and settle instead of passing through.

### Self-collision

At moderate densities, cloth points also avoid other nearby cloth points using a spatial hash. This is what keeps folds from collapsing into each other and helps the sheet bunch up naturally. Self-collision is the most expensive part of the simulation, so it is limited to the resolution range where it has the most visual benefit.

### Rendering

The cloth is a `THREE.BufferGeometry` with a position buffer and an index buffer. Its normals are recomputed every frame so the lighting follows the folds. The renderer uses anti-aliasing, soft shadow maps, a hemisphere light, directional lights, and a spot light in the Studio theme.

The backdrop is drawn onto an offscreen canvas and used as a texture. The Candy theme's colored circles are generated procedurally, so there are no image files to manage.

---

## Performance guide

Cloth simulation is CPU-heavy, and high-density rendering is GPU-heavy. If the frame rate drops, try these in order:

1. **Lower the polygon count.** This is by far the biggest lever. Going from 25,000 to 6,000 polygons usually feels much smoother.
2. **Use a smaller window.** The simulation cost stays the same, but fewer pixels make rendering cheaper.
3. **Close other GPU-heavy apps.** Browsers with many tabs, video players, and other 3D apps all compete for the same hardware.
4. **Lower the speed.** A slower simulation still runs every frame, but it gives each frame's constraints more visual time to settle and can make a heavy scene feel less frantic.
5. **Use the wireframe view.** It removes surface shading work and makes dense meshes easier to inspect.
6. **Turn off the stick.** The extra collision cylinder is small, but every constraint counts at high densities.
7. **Use the Ball or Cube shape.** The statue has more collision pieces than the simple primitives.

Integrated graphics can run the default scene comfortably. The 100,000-polygon setting is intended for machines with a discrete GPU, and even then the first drop may take a moment to settle.

---

## System requirements

| Item | Requirement |
| --- | --- |
| Operating system | Windows 10 or Windows 11, 64-bit |
| Graphics | A GPU with working WebGL support; integrated graphics is fine at moderate settings |
| Memory | A few hundred MB of free RAM is enough; high polygon counts benefit from more |
| Storage | About 72 MB for the executable, plus temporary space while it runs |
| Internet | Not required to play |
| Installer | Not required; the build is portable |
| Account | Not required |

The build is a portable Windows executable. It is not a native ARM build and it is not packaged for macOS or Linux.

---

## Troubleshooting

### Windows says "Windows protected your PC"

This is SmartScreen reacting to an unsigned executable. Click **More info**, then **Run anyway**. If you do not see **More info**, right-click the file, open **Properties**, tick **Unblock** at the bottom of the General tab, and try again.

### The window opens but the 3D view is blank

Make sure your graphics drivers are up to date. Drape needs WebGL; a machine running in a restricted remote-desktop session or with GPU acceleration disabled may not provide it. Try launching the app again, and try a lower polygon count if the view appears but is sluggish.

### The app is slow or the fans spin up

Lower the polygon count first, then reduce the window size. The 100,000 setting is deliberately demanding. See the [performance guide](#performance-guide).

### The cloth looks like it is stretching or jittering

Very large cloth sizes, fast speeds, and low polygon counts can produce exaggerated motion. Try a moderate cloth size and speed, and increase the polygon count a little. Jitter is also more visible when the cloth is nearly at rest; a slower speed can make the settle easier to watch.

### The cloth falls through the object

Collision is tuned for the objects and sizes in the panel, but extreme combinations can still produce tunneling, especially at high speed or with a very small object. Try a lower speed, a larger object size, or a higher polygon count.

### My settings were reset

Drape does not save settings between launches. Every time you open the app, it starts from the default Studio scene. There is no profile, save file, or cloud sync.

### The Play button stopped on its own

The automatic sequence stops when you change one of the scene-rebuilding controls, such as the shape, polygon count, object size, cloth size, drop offset, or stick, or when you press **Drop cloth**. That is intentional so the demo does not fight your manual edits. Press **Play 1 → 25000** again to restart it from the beginning.

### Antivirus quarantined the file

Unsigned portable executables sometimes trigger heuristic warnings. If you downloaded the file from this repository and your antivirus flags it, restore it from quarantine and add an exception only if you are comfortable doing so. Do not disable your antivirus globally.

### The taskbar icon or title looks generic

The build uses the plain Electron runtime icon. This does not affect gameplay.

---

## Privacy

Drape is an offline toy:

- No account or login
- No analytics, telemetry, or crash reporting
- No ads
- No online multiplayer or cloud features
- No network requests from the game code
- No saved personal data
- No access to documents, contacts, or other files

The executable's version metadata identifies the product only as "Drape". The game keeps its settings in memory for the current session and discards them when the window closes.

The repository contains only the playable build, its quick-start text file, and this README. It does not contain build logs, local file paths, personal email addresses, machine names, or machine-specific files.

If you fork or redistribute the build, keep the same courtesy: do not add personal information to the repository or the executable metadata.

---

## What is in this repository

| File | Purpose |
| --- | --- |
| `Drape.exe` | The portable Windows build. Double-click to play. |
| `README.txt` | The original two-line quick-start note included with the build. |
| `README.md` | This document. |

The repository ships the ready-to-run build only. It does not include the Electron project source, the `node_modules` folder, the `dist` folder, or the build scripts.

### Verifying the download

SHA-256 of the current `Drape.exe`:

```text
43E112CE9909053328F74509000882E10B872B4563DF43E8ECDDC8F9C60E701B
```

On Windows you can check a file's hash from PowerShell:

```powershell
Get-FileHash .\Drape.exe -Algorithm SHA256
```

The hash changes whenever a new build is uploaded, so compare it against the value in the README for the release you downloaded.

---

## Technical notes

- **Shell:** Electron 31
- **Renderer:** three.js r128
- **Physics:** Verlet-style particle integration with distance constraints
- **Collision:** analytic object tests for the statue, sphere, box, cone, cylinder, and torus
- **Self-collision:** spatial-hash neighbor search at moderate grid sizes
- **Cloth grid:** square grid, from 1 × 1 up to 316 × 316
- **Rendering:** WebGL with PCF soft shadows and procedural canvas backdrops
- **Packaging:** electron-builder portable target
- **Window:** 1100 × 800 by default, resizable, application menu removed

The simulation is intentionally self-contained. There is no asset pipeline, no texture files, and no external server. The visible scene is generated from geometry, colors, and canvas drawing code at runtime.

The 3D view uses a single perspective camera that orbits horizontally around a fixed look-at point near the center of the object. Dragging changes the orbit angle and clamps it to a little over ±1.3 radians, which keeps the camera from swinging behind the backdrop.

The cloth count shown above the scene is the true number of simulated polygons, not the target number in the input box. That is why typing 1,500 shows 1,521: the sheet has to be square, so the simulator rounds the grid to the nearest whole number of cells in each direction.

---

## FAQ

**Is Drape a game or a toy?**
It is a sandbox. There is no win condition, score, or timer. The **Play 1 → 25000** button is an automatic demo, not a challenge mode.

**Does it need an internet connection?**
No. The build runs entirely offline.

**Does it install anything?**
No. It is a portable executable. Delete the file when you are done with it.

**Can I run it on macOS or Linux?**
This repository contains a Windows build only.

**Can I save or export a cloth?**
No. Each drop exists only in the current session. There is no screenshot button, export, or save file.

**Why does the polygon count change after I type a number?**
The cloth is a square grid, so the simulator rounds your target to the nearest square number. The display above the scene shows the real count.

**Why is the statue the only shape with no stick?**
The statue already has a plinth and its own support geometry. The stick is meant for the simple shapes, where it adds a pole for the cloth to catch on.

**Can I use the mouse wheel to zoom?**
Not in this version. Dragging rotates the camera horizontally; there is no zoom control.

**Can I resize the window?**
Yes. The layout adapts, with the control panel moving to the right side on wider windows.

**Why does the cloth sometimes slide off?**
The cloth is a physical sheet, not a molded model. A small cloth on a steep shape, a large drop offset, or a fast drop can all make it slide. Try a larger cloth, a lower speed, or the stick.

**Why is the app unsigned?**
It is a small independent build. Code signing requires a certificate and an ongoing signing process. SmartScreen warnings are expected; use the **More info → Run anyway** path if you trust the source.

**Does the app collect anything about me?**
No. See the [Privacy](#privacy) section.

**Can I redistribute it?**
The repository does not include a license file. See [License](#license) for the current status.

---

## Credits

- **three.js** — 3D rendering library, MIT license
- **Electron** — desktop application runtime, MIT license
- **electron-builder** — packaging tool, MIT license
- **Drape** — concept, simulation, and build

The statue, shapes, cloth solver, themes, and interface are built specifically for this project. The background patterns in the Candy theme are generated procedurally with a small deterministic random-number routine.

---

## License

No license file is included with this repository, so no license is granted for the Drape game or its assets unless one is added later. The third-party components listed in [Credits](#credits) keep their own licenses.

If you would like to use the project in a way that is not covered by the default rules, open an issue to ask.

---

**Thanks for trying Drape.** If something looks wrong, or a particular shape and polygon count produces a great result, open an issue and describe what you did. A short note about your Windows version, GPU, and the polygon count is enough to make a report useful.
