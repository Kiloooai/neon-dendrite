# ⚡ Neon Dendrite

*Watch fractal dendrites grow via diffusion-limited aggregation. Particles randomly walk until they touch a cluster, then stick, forming lightning-branch structures. Click to add new seeds and watch competing dendrites. Neon glow, adjustable parameters. Mesmerizing emergent patterns.*

---

## What is this?

Diffusion-Limited Aggregation (DLA) is a process where particles undergoing random walks eventually stick to a growing cluster. The resulting patterns are the fractal-like branching structures you see in lightning, blood vessels, crystals, and coral. This interactive simulation spawns thousands of glowing walkers that adhere to the cluster, building organic dendritic forms in real time. You can add new seed points to spawn competing dendrites that eventually meet and merge.

---

## Features

- **Real-time DLA simulation** with random walkers and stick-on-contact
- **Neon glow** on every cluster point; colors evolve over time creating rainbow gradients
- **Multiple seeds** — click anywhere to plant a new cluster origin; watch dendrites expand and collide
- **Adjustable parameters:**
  - Max Walkers (10–1000) — cap on simultaneously active walkers
  - Spawn Rate (1–20) — how many walkers appear per frame
  - Stickiness (0.1–1) — probability to stick on contact; <1 produces spindly, tenuous branches
  - Step Size (1–8) — length of each random walk step; larger steps = faster but chunkier growth
  - Color Speed (0–2) — rate of hue cycling over time
- **Pause/Resume** and **Clear** controls
- **Stats overlay** — cluster size, active walkers, FPS
- **Single HTML file** — no dependencies

---

## How to Use

1. Open `index.html`
2. Watch a cluster grow from the center. Walkers (white dots) appear and wander randomly until they touch the cluster, then stick and glow.
3. **Click** anywhere on the canvas to plant a new seed. New dendrites sprout from that point and grow outward. When two dendrites meet, they connect.
4. Use sliders to change behavior:
   - **Max Walkers** — more walkers = faster growth, heavier CPU; fewer = slower, more meditative
   - **Spawn Rate** — how quickly new walkers are released
   - **Stickiness** — 1.0 means walkers always stick on first touch; lower values make them bounce off many times before finally sticking, creating finer, more tenuous branching
   - **Step Size** — walker step length; larger steps produce coarser, blockier clusters; smaller steps yield finer detail
   - **Color Speed** — how rapidly the color palette shifts over time
5. Press **Pause** to stop the simulation; **Resume** to continue
6. Press **Clear** to wipe the canvas and start fresh with a single central seed

---

## Technical Details

- **Algorithm:** Diffusion-Limited Aggregation (DLA) with off-lattice random walks.
- **Spatial indexing:** A low-resolution boolean grid (cell size ~3px) accelerates collision detection between walkers and the cluster. Each walker checks its grid cell for occupancy; if occupied, it may stick.
- **Cluster rendering:** Cluster points are drawn onto an offscreen canvas (`clusterCanvas`) as they are added. Each frame, this buffer is blitted onto the main canvas, avoiding O(N) redraw cost.
- **Walker motion:** Each walker takes steps of random angle and fixed length (`stepSize`). After each move, it checks its grid cell. If occupied, it sticks with probability `stickiness`.
- **Spawn logic:** Walkers spawn on a ring around the existing cluster (distance ≈ max cluster radius + 100px), chosen from random angles to ensure they approach from all directions.
- **Coloring:** New cluster points receive a hue based on the current global frame count multiplied by `colorSpeed`, producing smooth temporal color gradients.
- **Performance:** With `maxWalkers=1000` and cluster size up to ~20k points, the simulation runs comfortably at 60fps on modern hardware.

---

## The Real Story

DLA is a classic model of fractal growth in nature. The patterns that emerge are both mathematically beautiful and eerily familiar — they look like lightning, river deltas, crystals, and neurons. The neon glow turns the whole thing into a living neon organism. Adding multiple seeds creates competing colonies that eventually meet in intricate borders, like a silent war of expanding frontiers. Reduce stickiness and you get wispy, feathery structures; increase it and you get denser, more solid blobs. It's the simplest possible recipe for organic-looking growth, and it never repeats.

---

*Made with ⚡ and random walks.*

**Repo:** https://github.com/Kiloooai/neon-dendrite
