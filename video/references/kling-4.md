# Kling 4.0 reference (Kuaishou)

Read this instead of `kling.md` when the job runs on **Kling 4.0** (`kling-video-v4_0`). `kling.md` covers 1.x–3.0 and still applies to Kling 3.0 jobs, such as element takes.

Sources are tagged:

- **[Guide]** Kling's own 4.0 user guide (14 October 2026): https://kling.ai/quickstart/kling-4-model-user-guide
- **[MCP]** The Kling MCP model specification from `who_am_i` (MCP v1.3.3, 18 November 2026).
- **[Test]** A paid job on The Unreasonable Kitchen channel (job log in that channel's `kling-prompt-rules.md`, section 12).

## Contents

1. What changed from 3.0
2. Two entry points and what each can set
3. Prompt limits and shape
4. Keyframe takes
5. Omni-Ref
6. Camera
7. Sound
8. Failure modes and fixes
9. Skeletons

---

## 1. What changed from 3.0

| | Kling 3.0 | Kling 4.0 |
|---|---|---|
| Clip length | 3–15 s | 3–30 s in 1 s steps [MCP] |
| Frames | First + optional tail | First, tail and up to 10 in-between keyframes, 10 images in total [MCP] |
| Prompt input | 2,500 characters (API) | Up to 8,000 tokens [Guide] |
| References | Elements; video subjects | Omni-Ref: up to 15 inputs in total (10 images, 5 videos, 3 audio, 7 elements) [Guide, MCP] |
| Multi-shot | `prefer_multi_shots` true or false | Keyframe entry: no multi-shot setting. Omni-Ref: always true [MCP] |
| Flash tier | — | `kling-video-v4_0_flash`: 3–20 s, 720p, first frame only, no tail or keyframes [MCP] |

## 2. Two entry points and what each can set

### `image_to_video` · `kling-video-v4_0` (keyframe take)

- **Arguments:** `prompt`, `duration` 3–30, `resolution` 720p or 1080p (members), `imageCount` 1–4, `aspect_ratio` (leave it unset: the first frame sets it) [MCP].
- **Inputs:** `first_image`, `tail_image`, `keyframe_1`…`keyframe_10` in time order. All of them together count towards one cap of 10 images. Each image ≤ 30 MB, aspect 2:5 to 5:2. URLs only: from `file_upload` or a public URL, never a local path [MCP].
- **Not available:** negative-prompt field, camera-control setting, sound setting, keyframe timestamps, 4K, elements [MCP].

### `omni_ref_video` · `kling-video-v4_0` (references and elements)

- **Arguments:** `prompt`, `elements` (JSON `[{id, bindName, type}]`, at most 7 image and video subjects, at most 3 of them video), `duration` 3–30, `aspect_ratio` (auto when an image or video is given), `resolution`, `imageCount`, `prefer_multi_shots` (fixed at true), `enable_audio` or `keepOriginalSound` (only one of them true) [MCP].
- **Inputs:** `image_1`…`image_10`, `video_1`…`video_5` (each 3–30 s, all videos plus video subjects together 3–30 s), `audio_1`…`audio_3` (5–30 s each) [MCP].
- **Billing:** per second, and the length of any input video counts towards the billed time [MCP].

## 3. Prompt limits and shape

- **Input limit: 8,000 tokens** [Guide]. The guide doesn't say what happens to text past the limit, so treat anything beyond it as lost. Never write a prompt that relies on its tail end surviving.
- **Length follows the shot**, inside the limit. A short prompt gets expanded with Kling's own blocking and camera; a detailed one is followed closely [Guide]. A one-or-two-sentence limit was tried on the channel and withdrawn [Test].
- **Describe the motion and the change, not the still.** The frames carry the look. Re-describing what an image already shows can make identity or details drift [Guide, via Krea's 4.0 guide].
- **Descriptive language, few abstractions, few negatives.** Kling says negative instructions can increase errors [Guide]. Exceptions that work: "no subtitles", "no background music", and a specific exclusion next to its positive ("one continuous master shot, no cuts") [Guide].
- **Counts and precise adjectives get drawn literally.** "A few small flakes" became one large chunk; "two bones" became one [Test]. Keep quantities in the frames. "Exactly one" is fine for a single hero subject [Guide].
- **Prose.** No JSON.

## 4. Keyframe takes

- **Each keyframe ends a segment.** Kling invents how the segment starts and moves the camera towards the keyframe, even against "fixed camera" [Test]. A segment with no keyframe near its start opens on an invented framing [Test].
- **Spacing is even.** The MCP has no timestamps; three frames in a 15 s take landed at 5.04 s and 10.08 s [Test]. Shift timing by adding or removing frames, not by wording.
- **Say whether you want cuts.** For one take, write that it "must be one continuous master shot with no visible cuts" [Guide]. A 30 s MCP take asked this way came back with no cuts [Test]. The web app cut hard at each keyframe [Test].
- **Keep neighbouring keyframes close** in composition and state. A big jump (day to night) belongs in two clips [Guide, via Krea].
- **Build every keyframe as an edit of one base image.** Objects that differ between frames merge or swap: two wings became one [Test].
- **Show what holds every object up.** Wings with no visible contact lifted off the plate [Test].
- **Start and end frame on every take.** A first-frame-only take invents the ending [Test].
- **A subject in the end frame needs a visible path in:** in the start frame already, or entering at a frame edge. Otherwise it appears mid-air [Test, on 3.0].
- **An end frame that is a crop of the start frame reads as a zoom.** Write "zooms in", not "pushes in" [Test].
- **Small moves finish fast and hold.** Plan to retime in the edit [Test].

## 5. Omni-Ref

- **Reference syntax:** images as `图片1`…`图片10`, videos as `视频1`…, audio as `音频1`…, elements as `<<<id>>>` with the id listed in `elements` [MCP]. `@Image1`-style names are not the MCP's syntax.
- **Give each reference a role** in the prompt ("图片1 is the Dutch oven; keep it exactly as shown"). Without a role, Kling guesses what it's for [Guide].
- **Always multi-shot.** A single continuous take with an element isn't possible on 4.0 Omni-Ref [MCP]. For a single take holding a character, Kling 3.0 `image_to_video` with an element and `prefer_multi_shots=false` held on the channel [Test, on 3.0].

## 6. Camera

- **Name the camera mode in plain words:** fixed camera, slow push-in, pull-back, pan, lateral tracking, orbit, top-down overhead [Guide].
- **"Fixed camera" held** a 12 s, 2-frame take where only colour changed [Test], and 0 px over 5 s on 3.0 [Test].
- **Reframes come from keyframes.** Kling's guide also allows a timestamp in words ("at 8 s the camera eases left") [Guide]; whether it moves keyframe timing is untested.
- **Gear words:** Kling's guide names gear to exclude it ("not a gimbal or slider") [Guide]. On Veo, naming gear drew it into the shot. Untested on Kling: follow the project's banned-word list until it is.

## 7. Sound

- **Keyframe takes always generate sound.** There is no setting on that entry [MCP].
- **Music can appear by default.** End prompts with "No background music, no subtitles." [Guide].
- **Omni-Ref:** `enable_audio` for new sound, or `keepOriginalSound` to keep the reference video's [MCP]. Up to 3 audio references for voice and sound [MCP].
- Whether sound words in the prompt steer keyframe-take audio is untested.

## 8. Failure modes and fixes

| Failure | Fix |
|---|---|
| Opening framing invented, camera drifts towards the first keyframe | Put a keyframe near each segment's start, or use a locked 2-frame take |
| Objects merge, swap or morph between keyframes | Edit every keyframe from one base image; diff objects frame by frame |
| Object lifts off its surface | Show the contact point in every frame |
| Invisible things (air layers, heat) drawn as solids | Never draw them in a frame or name them in the prompt; add graphics in the edit |
| A subject pops in mid-frame | Give it a start position in the first frame or an entry at a frame edge |
| Hard cuts on a take meant to be continuous | "One continuous master shot with no visible cuts" |
| Colour shifts inside a long take | Check the whole take; match in the grade |
| Counts or precise adjectives misdrawn | Put the quantity in the frames; describe the motion only |
| Background music or subtitles added | End with "No background music, no subtitles." |

## 9. Skeletons

### Locked 2-frame take

```text
{Subject} {does the motion}, seen from a fixed camera{, further detail the shot needs}. Everything else stays exactly as in the first frame. No background music, no subtitles.
```

### Continuous keyframe take

```text
{What happens across the take, in time order, describing the motion between frames}. The camera {camera behaviour}. This must be one continuous master shot with no visible cuts. No background music, no subtitles.
```

### Omni-Ref with an element

```text
图片1 is {what it is}; keep it exactly as shown. <<<{element id}>>> {does the motion}. {Camera behaviour}. No background music, no subtitles.
```

---

*Kling 4.0 reference written for the ebotha9 fork. Upstream skill: Serge Shima — github.com/smixs/visual-skills · License: CC BY 4.0*
