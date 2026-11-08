Builds an interactive particle-portrait web page from a user's photo - the photo becomes thousands of colored particles that scatter away from the mouse arrow or a finger touch and spring back into the picture. Use this skill whenever the user wants to make a photo, selfie, portrait or logo interactive, asks for a particle simulation, particle effect, "particles that move when I touch or hover", or wants an image to react to the cursor, even if they don't say "skill" or "canvas".

Particle Portrait

Role: senior creative front-end engineer who builds smooth canvas animations in plain HTML, CSS and JavaScript.

Goal

One interactive page. The user's photo is converted into thousands of particles that react to the mouse arrow and to finger touch on mobile.

Workflow
Locate the user's photo (usually in /mnt/user-data/uploads). Never modify or rename the original.
Create a project folder with assets/photo.jpg (copy the photo there; if it is large, a resized COPY at about 540x960 max is fine for speed).
Copy the three files from assets/template/ (index.html, style.css, script.js) into the project root. Deliver exactly these three files plus the photo. No frameworks, no build step, no npm.
Only edit the constants at the top of script.js if the user asks for a different feel.
Deliver:
If the user wants a link or a single file: build one self-contained HTML (inline the CSS and JS, embed the photo as a base64 data URI, resized to about 540px wide JPEG) and publish it with the Artifact tool. A page that loads ./assets/photo.jpg will NOT work as an artifact.
If the user wants project files: present the folder files and give the one command python3 -m http.server 8000 and the URL http://localhost:8000.
After each step output: ✅ [what was completed].
Behavior (all MUST be true)
Draw the photo to an offscreen canvas scaled to fit the viewport, keeping aspect ratio. Sample on a grid (STEP 4 to 6 px). One particle per sampled pixel that is not near-transparent.
Each particle stores home position, current position, velocity and original RGB. Draw as 2 to 3 px squares or circles in the original color so the portrait is recognizable at rest.
Pointer within about 90 px pushes particles away; strength falls off with distance; nearby particles visibly scatter.
Spring force plus friction pulls every particle home, so the portrait re-forms in about 1 second after the pointer leaves.
Touch: pointermove and touchmove drive the same interaction; touch-action: none on the canvas.
Click or tap triggers a stronger outward burst.
requestAnimationFrame, one 2D context, clear and redraw each frame, particle data in Float32Array.
Canvas fills the window, re-samples on resize, handles devicePixelRatio.
Background 
#0a0a0a. No text, buttons or UI.
Tunable constants (top of script.js)

STEP, PARTICLE_SIZE, MOUSE_RADIUS, PUSH_FORCE, SPRING, FRICTION, BURST_FORCE.

Constraints
Deliver only what is listed. No extra features, libraries or refactors.
Log a console error if the image fails to load.
Keep physics code commented in plain language.
Done when
The portrait appears as particles, mouse movement scatters nearby particles, and they return within about 1 second.
Touch on a phone works without scrolling the page.
About 60 fps with 10,000+ particles (raise STEP if the photo yields too many).
Content