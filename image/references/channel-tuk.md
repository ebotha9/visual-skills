# Channel overlay: The Unreasonable Kitchen

Load this file **last** whenever the image is for The Unreasonable Kitchen (YouTube channel): Set Bible masters, Prop Bible sheets, the Hands sheet, start frames, keyframes, end frames and thumbnails. It overrides anything else in this skill.

## 0. Precedence

1. The channel's project instructions, `preflight-gate.md` and `kling-prompt-rules.md` (in the project's `Production/Prompt library/`) win over everything in this skill.
2. This overlay wins over the rest of this skill.
3. Then the skill's own files.

If this overlay and the channel docs disagree, the channel docs win. Flag the gap so this file gets fixed.

## 1. Model and reading order

- **Frames come from FLUX** through the FLUX MCP (`generate_image`), not Nano Banana or GPT Image. Replace steps 1 and 2 of `SKILL.md` with the FLUX MCP's `flux-image-best-practices` skill (call `get_skill`), including its I2I and multi-reference sections. FLUX takes no negative prompt: describe what the frame contains.
- **Still read:** `golden-rules.md`, `editing.md` for every edit, `de-slop.md` for every grounded frame, and `characters.md` for the bee or the hands across a series of frames.
- **Not used:** the food and beverage, fashion and e-commerce pattern libraries. They aim for ad and poster polish, the opposite of the channel's look. Nano Banana and GPT Image model rules don't apply to FLUX jobs.

## 2. Every frame starts from a locked source

- **Set:** every grounded frame is derived from a Set Bible master by editing. Never a fresh text-only kitchen.
- **Props:** reuse the Prop Bible one-line spec word for word. Check the base photo against its Prop Bible sheet before editing (round 1 had the wrong air fryer basket).
- **Hands:** only from the Hands sheet, partly out of frame.
- **Keyframes and end frames are edits of one base image.** Objects that differ between frames merge or swap in the video (two wings became one).
- **Start frame edited from end frame** (or the other way round) when something moves position, so everything else matches pixel for pixel.

## 3. Edits

`editing.md` and `golden-rules.md` §3 ("edit, don't re-roll") apply, with these channel rules from the pre-flight gate:

- **One change per edit.** Lock the objects in one edit, then reframe in the next.
- **Write the full end state, not just the change.** For anything a hand holds, the hand keeps the same grip on the same part. For food, name the cut, the mix and the colour ("flats and drumettes with pale pink skin"), never just "raw wings". FLUX fills gaps with its own guess.
- **Edits that move one object can move its neighbours** (FLUX lowered a probe thermometer along with the tongs, twice). Diff every region of the edited frame against its partner, not only the action area.
- **Never re-roll an approved image.** Fix only the failed region.

## 4. De-slop, applied to this kitchen

`de-slop.md` applies to every grounded frame:

- **Capture pipeline:** state it as a fact. "Shot by a home cooking creator on a full-frame mirrorless camera with a 35 mm lens" (or a 100 mm macro), natural exposure, subtle sensor noise, no film grain, no HDR look, framing a touch off-centre. This matches the approved Prop Bible prompts.
- **Located imperfections go on the set, not the tools:** flour dust on the counter, a crumb near the board, a tea towel where it was dropped, faint water rings near the sink. **Cookware and tools stay clean** (no drips, streaks or stains) unless the script makes the mess part of the action.
- **"Crisp" and "golden"** are allowed as food texture and colour words. They stay banned as quality boosters ("crisp focus", "crisp detail").
- **Steady and sharp on the subject.** "Not too perfect" means a lived-in set, never camera faults: no blur, shake or soft focus on the subject.

## 5. Physics in the frame

- Each keyframe shows the true state at its moment.
- Invisible things (air layers, heat, convection) are never drawn. They go in the edit as graphics.
- Steam only from a real opening, in the amount the heat gives. Frames show less steam than wanted.
- Show what holds every object up: the contact point is visible in every frame.
- Nothing in the frame waits for a hand: a lit burner with an empty grate and a pot beside it reads as a cook mid-task, and the video model adds the cook.
- Salt stays at the locked size: coarse sea salt, 2–3 mm crystals.
- Quantities live in the frame, never in a later prompt.

## 6. Words and marks

- **No text, logos, wordmarks or trade dress.** Props are unmarked. Every label and readout is added in Resolve. (`text-rendering.md` is used only for thumbnails, and only if Elmer asks for text in the image.)
- **US details:** US outlets and switches, a range with front knobs, °F oven, US cups and spoons.
- **Gear:** the capture camera may be stated as the capture pipeline. No other gear words (tripod, light stand, softbox, boom, mic): they draw the object into the frame.

## 7. Output and hand-off

- Output per `SKILL.md`, with `Model: FLUX (via FLUX MCP)` and the edit's Change / Preserve list.
- Frame resolution: 16:9 (or 9:16 for native vertical), wide enough for 1080p video without upscaling.
- **Never run a generation from this skill.** Every frame goes through `tuk-kling-preflight` (Bible check, object inventory diff, misread test), and Elmer confirms the exact prompt before it runs.

---

*Channel overlay for the ebotha9 fork. Upstream skill: Serge Shima — github.com/smixs/visual-skills · License: CC BY 4.0*
