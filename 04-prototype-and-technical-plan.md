# Prototype and technical plan

## Current artifact
An offline, zero-dependency HTML storyboard in `storyboard.html`. Clickable narrative scenes and simple decisions; not a rendered 3D simulation.

## Suggested phases
**Phase A: story UX** — Polished clickable storyboard and visual mood/character exploration. Validate story pacing and first loop with parents and children.

**Phase B: playable 3D vertical slice** — One environment, Pip + cautious rider + two supporting cast characters, one buildable coaster, one ride camera, small library of curated reactions, Spark UI, and 2–3 cosmetic attachments.

**Phase C: bounded creation / voice** — Grammar or intent classification → validated game commands → procedural construction, with preview/undo and budget/physics limits. No uncontrolled runtime generation or arbitrary content for children.

**Phase D: expanded sandbox** — More track pieces, varied camera perspectives, additional worlds and authored character arcs, once the vertical slice validates.

## Engine recommendation (tentative, needs benchmarking)
- **Browser-first demonstrator:** React + React Three Fiber + Three.js, assets in glTF/GLB, physics if needed (Rapier). Fast iteration and shareable URLs; particularly good for a narrow browser vertical slice.
- **Alternative for a fuller native 3D game:** Unity with URP (especially if iPad performance, animator tooling, asset pipelines and more ambitious scenes dominate). Godot is another option worth evaluating for tooling and licensing.
- **Decision criteria:** character animation fidelity, iPad framerate, pipeline from Blender, shader/lights quality, texture/memory budget, iteration speed, accessibility, build distribution, team skills.

Nothing in our prior discussion establishes Three.js as the final engine choice; it is a pragmatic experiment, not a commitment.

## Character art pipeline: sketch to expressive real-time 3D
1. **Character bible:** silhouette thumbnails, shape language, proportions, color palettes, motivations, emotional range, accessories.
2. **2D concept sheets:** front/side/back turnarounds, pose sheets, facial expression sheets, lighting/material references.
3. **Blockout:** sculpt/model low-resolution body volumes in Blender or equivalent; review silhouettes at thumbnail size and in-game camera distance.
4. **Refine:** sculpt stylized facial forms, clothing and hair/creature details. AI-assisted sketch/3D exploration is optional, but expect substantial manual cleanup and art direction.
5. **Game topology:** retopology, UVs, texture baking, efficient materials, LODs/texture atlases for target hardware.
6. **Rig:** skeletal body controls, face blendshapes or bone-based expressive facial rig, sockets for hats/capes/props.
7. **Animation library:** idle, locomotion, anticipation, fear, joy, laugh, surprise, fall/recover, ride cycle, accessory gags. Prioritize readable posing, timing and silhouettes.
8. **Export:** standardized GLB/glTF or FBX based on runtime. Confirm skeletal and facial animation, material compatibility, transforms and attachment points.
9. **In-engine lookdev:** environment lighting, stylized shaders, shadows, color grading, postprocessing tuned for performance. High-end *offline* film render quality is not an appropriate runtime target.
10. **Test:** real-device performance, draw calls, animation blends, clipping, facial readability at common camera distances, frame stability.

## Runtime architecture (conceptual)
Input (touch / bounded voice) → intent mapping → approved command schema → construction validator (safety/physics/game limits) → coaster/world state → simulation/playback → authored reaction selection → collectible/reward logic → persistent customization.

Possible construction commands: `ADD_TRACK(segment_type, snapped_anchor)`, `ADJUST_HEIGHT(target, clamped_value)`, `ADD_THEME_OBJECT(asset_id, approved_socket)`, `START_RIDE()`, `EQUIP_ACCESSORY(character_id, accessory_id)`.

Use controlled animation/reaction assets with a finite state machine or behavior graph. If a language model is used, it must not directly emit executable code or arbitrary on-screen speech for children; validate intent and select safe authored responses.

## Technical prototypes to de-risk first
- One stylized character in real-time with compelling face and body reactions.
- A one-minute coaster ride with believable camera, readable excitement and performance on a representative tablet.
- Reliable accessory sockets and animations (hat doesn't clip wildly).
- Deterministic editor actions and undo.
- Asset budgets for target platform (to be determined by measurements, not guessed upfront).

## Not yet produced
No final concept art, turnaround sheets, rigs, animations, 3D models, sound design, level design, full working game, repository or deployment has yet been produced through this conversation.