# Wind ribbons in 3D

A small three.js demo of Windy-style wind trails drawn as real 3D ribbons over terrain.

**Live demo:** https://goharayub3909-stack.github.io/wind-ribbons-demo/ (after you turn on GitHub Pages)

The wind and the terrain are **synthetic**: a rotating north-westerly with one swirl, plus a simple terrain effect that blocks and turns the flow and speeds it up over high ground. The demo is for judging how the trails look. It is not real forecast data and not meteorology.

## Controls
- Drag to rotate, scroll or pinch to zoom, right-drag or Shift-drag to pan.
- **Windy-like trails** and **Current portal look** switch between long tapered trails and short uniform dashes on the same wind.
- Sliders: particle count, trail length, wind speed scale, terrain effect on the wind, head width, height above ground, terrain brightness.
- Options: dark outline under the trails, colour by speed, hide trails behind ridges.
- The panel shows the typical trail length in pixels at the current zoom.

## How it works
- Each particle records its recent 3D positions into a ring buffer, one point every 1/20 s of simulated time, so a trail's length follows the wind speed and does not depend on the screen's refresh rate.
- Each trail is drawn as a camera-facing ribbon built in a custom vertex shader: about 3.2 px wide at the head, 0.5 px at the tail, with the opacity fading along its length. A darker, wider copy of the same geometry is drawn underneath as an outline.
- Trails live in world space and are depth-tested against the terrain, so they stay put while you orbit and ridges hide them.
- Face culling is turned off. All the ribbon triangles share one winding, and with the default culling almost every trail disappears.
- Particles are respawned evenly across the map with a Halton sequence, and fade in and out, to avoid clumps and popping.

## Running it
It is one self-contained file. Open `index.html` in a browser, or serve the folder with any static server. It needs WebGL and an internet connection, because it loads three.js (r128) from cdnjs and a font from Google Fonts.

## Notes
- Tested in a software-rendered headless browser, so frame rates on a real GPU are unmeasured. Lower the particle count if it stutters.
- Touch controls (rotate and pinch) are untested.
- Licence: none chosen yet. Add a `LICENSE` file (MIT is a common choice) if you want others to reuse the code.

## Credits
three.js (MIT licence), loaded from cdnjs. DM Sans, loaded from Google Fonts.
