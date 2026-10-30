# EDIT BRIEF — Instagram Reel IMG_1541.MOV

Paste into Claude Code after setup is done. Change the footage path to where the file is.

---

- **FOOTAGE:** `/mnt/c/Users/<you>/Videos/IMG_1541.MOV` (work on a copy)
- **PLATFORM + LENGTH:** Instagram Reel 9:16, under 20 s (about 18 s after trims)
- **GOAL:** viewer watches to the end, rewatches, and comments or saves
- **BUDGET FOR PAID AI:** £0 (no Higgsfield/OpenMontage generation)

Follow the workflow in CLAUDE.md. Tools: ghost-editor (main editor), claude-video-effects (`/effects`), earshot (MCP), Real SFX with `~/SFX`.

## Everything already known about this clip (verify, don't redo)

| Item | Value |
|---|---|
| File | IMG_1541.MOV, iPhone, 27.6 MB |
| Length | 19.2 s |
| Video | 1080×1920 vertical, 30 fps, HEVC (H.265) |
| Audio | AAC stereo, 44.1 kHz |
| Loudness | −28.4 LUFS integrated, max −9.5 dB (very quiet; target −14 LUFS) |
| Shot | ONE continuous static shot, no cuts, camera on a fixed stand |
| Framing | Speaker seated, framed knees-up, face in the upper third, centred |
| Movement | Hand gestures at about 4–7 s and about 17 s; otherwise still |
| Light | Bright window behind the speaker; face slightly underexposed |
| Background | Busy: laptop on a white desk, red flowers, plastic bottles bottom-left, hanging ornament, clothes on the right |
| Room sound | Indoor room; likely echo |
| Pauses (silence ≥ 0.3 s at −40 dB) | 0.00–0.39 (dead air at start), 4.98–5.33, 7.46–7.80, 15.29–15.61 |
| Spoken parts | A 0.39–4.98 · B 5.33–7.46 · C 7.80–15.29 · D 15.61–19.20 |
| Words | Not yet transcribed — transcribe first |

## Phase 1 — Transcribe and plan, then STOP

1. Transcribe with word timestamps.
2. Beat sheet table: time · exact words · beat type (hook / stakes / value / peak / CTA) · psychology lever · visual · effect + exact command · sound · on-screen text.
3. 3 on-screen hook lines (3–6 words, curiosity gap) from what is actually said in part A. Never change the spoken facts or invent numbers.
4. Name the single strongest line for the "peak" (should land around 70–80% through).

Wait for "go".

## Phase 2 — Edit in passes (look at frames after each)

1. **CLEAN CUT:** cut the 0.39 s of dead air so the first frame is already speaking. Tighten each pause to about 0.12 s. Remove false starts and "um"s.
2. **MOVEMENT** (the camera is static, so the edit must create it): cut at each of the 3 pauses, alternating framing 100% ↔ about 115% punch-in, face-centred. `/effects lean-in` on the most important word in part C. `/effects slow-push` on part D. A visual change every 2–4 s.
3. **HOOK** (first 1.5 s): big kinetic text of the chosen hook line in the top third, never over the face, with a sound hit on the first word. If part A asks a question or makes a bold claim, use `/effects backdrop-word` with its key word behind the head.
4. **HERO EFFECT:** at most 2 in the whole reel, matched to the words:
   - a list → `/effects todo`
   - a myth or "don't do this" → `/effects reject-stamp`
   - a number or cost → `/effects liquid-glass-graph` (real numbers only — ask me)
   - a chat or story moment → `/effects messages`

   Put one on the peak line. Never two within 6 s.
5. **CAPTIONS:** ghost-editor clean preset. 2–4 words per caption, one highlighted key word, placed at about 58–68% of frame height (chest), clear of the face, Instagram's bottom 20% and the right-side buttons.
6. **LOOK:** lift and warm the face, pull down the window highlights, lightly blur or darken the background so the clutter fades and the face pops. Natural skin tones, no heavy filter.
7. **SOUND:**
   - Voice: denoise (DeepFilterNet), reduce room echo, compress; final mix −14 LUFS, true peak ≤ −1 dB.
   - SFX from `~/SFX` only, 4–6 total: a soft hit on the hook, a whoosh or pop on each punch-in cut, a small pop when captions or effects appear, a riser into the peak.
   - Music: quiet modern light-beat instrumental (licensed or my library), ducked about 18 dB under the voice; drop it for about 0.3 s just before the peak line.
   - ONE sound owner: ghost-editor's mix or Real SFX, not both.
8. **ENDING:** last 1–2 s either loops into the first frame (end on a line that leads back into the hook) or shows a specific comment CTA ("Comment X and I'll send you…"). Suggest which fits the words.

## Phase 3 — Self-review

`earshot critique` and `timeline` (loudness, every SFX on its cut, voice clarity). Check the face is never covered, captions are readable on a phone, no dead air, length ≤ 20 s. Fix, max 3 rounds.

## Phase 4 — Deliver

- Final MP4 (1080×1920, H.264, Instagram spec) and SFX stem WAV
- Cover frame suggestion with title text
- Post caption (2 lines + 3–5 hashtags)
- 3 hook-text variants as separate first-2-second versions for A/B testing
- 5 moments to check by ear

**Rules:** never invent numbers or quotes; only sounds and music I have rights to; ask before anything irreversible.
