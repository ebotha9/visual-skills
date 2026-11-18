# Channel overlay: The Unreasonable Kitchen

Load this file **last**, after `dramaturgy.md`, `universal-rules.md` and the model file, whenever the work is for The Unreasonable Kitchen (YouTube channel). It overrides anything above it.

## 0. Precedence

1. The channel's project instructions, `kling-prompt-rules.md` and `preflight-gate.md` (in the project's `Production/Prompt library/`) win over everything in this skill.
2. This overlay wins over the rest of this skill.
3. Then the skill's own files.

If this overlay and the channel docs disagree, the channel docs win. Flag the gap so this file gets fixed.

## 1. What this channel is

- Food science explained in one real, lived-in American home kitchen. Faceless. One consistent pair of hands, only from the Hands sheet.
- Footage must look like a talented creator shot it with one full-frame mirrorless camera (35 mm lens, 100 mm macro), not like cinema. Impossible Kitchen shots (inside the food, scale shifts, time reversed) may be fully cinematic, but their physics must be true.
- The director earns the view; the scientist earns the return visit. No result is faked or exaggerated for drama or a joke.

## 2. Reading order and model choice

- **Model file:** Kling 4.0 jobs read `kling-4.md`. Kling 3.0 element takes (for example the bee) read `kling.md`, sections 3 and 7. FLUX video jobs (free generations only) follow the FLUX MCP's own `flux-3-keyframes-continuation` and `flux-3-prompting` skills. Seedance and Veo files are not used.
- **Task files:** `role-modes.md` for shot lists. `fixes-and-skeletons.md` for diagnosing a failed take. `camera-lighting-vocabulary.md` only for words allowed by section 6 below.

## 3. Dramaturgy, read for a faceless food channel

`dramaturgy.md` assumes actors. Apply it this way:

| Skill concept | On this channel |
|---|---|
| Hero's desire | What the food or the cook is trying to reach: crisp skin, a clean pull, a set custard |
| Obstacle | The physics in the way: water in the skin, heat that can't get in, sugar past hard crack |
| Space geometry | The Set Bible zone and screen direction (pours and movement keep one direction; 180-degree rule) |
| Controlled gaze | One focal point per frame: the food at the moment of change |
| Editing rhythm | Section 5 below |
| Physical micro-action on the body | **A change in the food's state**: fat rendering, an edge browning, bubbles from the food, a crack opening. Hands only when the shot needs them, from the Hands sheet |
| Environmental pressure | A real source in the kitchen: window light, the hood lamp, the hob glow, room tone. Steam only under section 7 |
| Sound or visual motif | The episode's recurring motif (see five anchors) |
| Power and staging (sections 5–6) | Not used: no characters to stage |

**Five anchors per episode** (`dramaturgy.md` §13): name one emotion, one visual motif, one anchor object, one break and one final image in the beat sheet. The break is the midpoint turn of the episode architecture. The final image is the payoff plate.

**Three jobs** (`dramaturgy.md` §3) is the channel's "every shot has a job": establish, reveal, explain, escalate or pay off.

## 4. Universal rules: what changes

| Rule | Override |
|---|---|
| U1 skeleton | Kling 4.0 prompt shape in `kling-4.md` §9 and the channel rulebook, section 5 |
| U5 camera move | One move at most; **never shake**. No "slight handheld shake" on grounded shots. Any sway is described, small and smooth |
| U6 lens | 35 mm and 100 mm macro are the creator's kit. No anamorphic, drone or crane looks on grounded shots |
| U7 identity anchor | No faces. Props: reuse the Prop Bible one-line spec word for word. Hands: the Hands sheet. Quantities live in the frames |
| U9 consequence prompting | Allowed when the end frame shows the consequence ("the bubbling dies away" when the end frame is calmer). Name the motion, not the mechanism |
| U10 duration | Kling 4.0 takes run 3–30 s; continuous takes through keyframes are planned. Shot length on screen still follows the edit rhythm |
| U11 final image | The end frame is the final image. Every take has a start and an end frame unless Elmer says otherwise |
| U12 three-detail check | Run it with the table in section 3. A grounded shot's "micro-action" is the food's state change |
| Dialogue | None in grounded shots: speech invites a person into the frame. Narration and the bee's lines are recorded separately and laid in the edit |

## 5. Rhythm

- `dramaturgy.md` §12's rhythm ladder applies, with the pause before the impact. That pause is the channel's Villeneuve hold and the half-second of nothing after a comedy punch.
- Fast sections change scale or motion every 3–6 seconds. Re-hook every 45–60 seconds.
- Vary shot lengths so the cut doesn't fall into a steady 4/6/8-second rhythm, which reads as generated.
- Murch's Rule of Six (`dramaturgy.md` §4) is the priority order for every cut in the edit review.
- Shot cards (`dramaturgy.md` §11) feed the shot list. Keep the **Eye trace** and **Cut type** fields.

## 6. Words

- **Banned in prompts** (the channel rulebook, section 11): tripod, slider, gimbal, rig, crane, dolly, jib, Steadicam, stabilizer, handheld, hand-held, camera operator, operator, crew, cameraman, light stand, softbox, C-stand, boom, microphone, mic, clapper. Describe the motion instead ("the camera slowly pushes in", "with a slight, natural sway"). The rulebook is the live list; if it changes, it wins.
- **Banned as empty praise** (`dramaturgy.md` §2): cinematic, professional, high quality, masterpiece, stunning, epic, premium.
- **Never the human cause:** no "just dropped in", "freshly cracked", "just set down". Describe the state.
- **Counts:** never above one in a prompt. Quantities live in the frames.
- **Comparisons** get drawn literally ("like a building" becomes a building). Use them only in narration, never in a prompt.
- **Standing tail:** every prompt ends "No background music, no subtitles."

## 7. Physics and known failure points

- Invisible things (air layers, heat, convection) are never drawn or named as objects. They go in the edit as graphics.
- Steam comes only from a real opening, in the amount the heat gives, with its size in plain words ("a few faint wisps"). Frames show less than wanted.
- Liquids: short pours, cut on contact. Oil tints everything amber. Bubbles in frying oil come only from the food.
- Tearing and cutting start from food already torn or cut.
- Growth (blisters, foam, browning) overshoots: make the last frame the peak.
- No generated text, labels or logos. Every readout is added in Resolve.
- Cookware and tools stay clean unless the script makes the mess part of the action.

## 8. Output and hand-off

- Deliver: the shot card, then the prompt, then the frame list (start, keyframes, end) with what each must show.
- **Never run a paid job from this skill.** Every prompt goes through `tuk-kling-preflight` (the pre-flight gate), and Elmer confirms the exact prompt before any credits are spent.
- Refer to shots by what they show, not by internal codes.

---

*Channel overlay for the ebotha9 fork. Upstream skill: Serge Shima — github.com/smixs/visual-skills · License: CC BY 4.0*
