# Phase 1 plan — "3 things before Oxford Street" reel

Source: the 39 s clip uploaded earlier (`5faa3b59-….mp4`). `IMG_1541.MOV` from the brief was never uploaded, so this plan follows the same CLAUDE.md workflow on the clip that is here.

## Phase 0 — Check

| Item | Value |
|---|---|
| Video | 576×1024 (9:16), 30 fps, H.264 — low resolution, so the final export is upscaled to 1080×1920 and punch-ins are capped at ~110% |
| Length | 39.4 s, of which 37.3–39.4 is the CapCut outro (black) |
| Audio | AAC, −25.3 LUFS integrated, true peak −7.1 dBTP (quiet; target −14 LUFS / −1 dBTP) |
| Shot | Two people seated side by side; she (left) opens and closes, he (right) talks through the middle. Handheld/phone on a stand: the framing slowly drifts tighter on him |
| Faces | Both in the top 15–45% of the frame. Text goes in the top 0–14% band or at chest height (58–68%); never between |
| Background | Bright window behind, red roses, bottles on the desk |
| Speech (VAD) | A 0.18–2.98 · B 3.51–5.54 · C 5.85–11.53 · D 11.77–16.33 · E 16.82–19.97 · F 21.18–24.42 · G 24.89–27.37 · H 28.70–29.16 · I 29.43–35.62 |
| Pauses to cut | 2.98–3.51, 5.54–5.85, 11.53–11.77, 16.33–16.82, 19.97–21.18, 24.42–24.89, 27.37–29.43, 35.62–end |
| Tools here | ffmpeg ✓, Whisper (turbo, via sherpa-onnx) ✓, Epidemic Sound connector ✓ (licensed music + SFX). Not available in this cloud session: ghost-editor, `/effects`, earshot, Openverse |

## Transcript — PLEASE CONFIRM

Whisper only partly handles the Hindi/English mix (it cuts off Hindi lines), so these are **best readings, not exact quotes**. Gaps and guesses are marked. Captions and hook text will only use words you confirm.

| Part | Time | What I hear (Hinglish) | Meaning (English) |
|---|---|---|---|
| A | 0.18–2.98 | "Oxford Street jaane se pehle, teen baatein sun lo…" | "Before you go to Oxford Street, listen to three things" |
| B | 3.51–5.54 | "Pehli baat, yahan pe … [?]" | "First thing: here … **[unclear — what is thing 1?]**" |
| C | 5.85–11.53 | "…jisse ki Christmas dekhne ka maza hi alag hoga, kyunki ab hum sadak… [?]" | "…which makes seeing Christmas a whole different fun, because now we… **[unclear]**" |
| D | 11.77–16.33 | "London ki Selfridges ki windows mein … shehar ke alag … [?]" | "In London's Selfridges windows, every one is different … **[unclear]**" |
| E | 16.82–19.97 | "aur traffic cones se … Christmas tree bhi hai" | "and there's a Christmas tree made of traffic cones" |
| F | 21.18–24.42 | "Aur teesri jo ki sabse aakhri aur sabse badi…" | "And the third, the last and the biggest…" |
| G | 24.89–27.37 | "Harry Potter ka sabse bada store/showroom…" | "Harry Potter's biggest store" |
| H | 28.70–29.16 | (half a word — false start) | — cut |
| I | 29.43–35.62 | "…uske andar ek Harry Potter wali night bus bhi hogi, toh hum sab ja rahe hain… aage ki details ke liye follow karo" | "…inside there'll be a Harry Potter night bus too, so we're all going… follow for more details" |

**Questions:** (1) What is thing #1 (parts B–C)? (2) Is G the Harry Potter store on Oxford Street? (3) Captions in English (translated) or Hinglish (romanised)? (4) Who is in the reel, so I name you correctly in the post caption?

## Beat sheet (times are after the clean cut, ≈ 31 s total)

| Out time | Words (from above) | Beat | Psychology lever | Visual | Effect / exact command (ffmpeg here) | Sound | On-screen text (top band) |
|---|---|---|---|---|---|---|---|
| 0.0–2.8 | A: "Before Oxford Street, 3 things" | Hook | Curiosity gap + triple hook | Start at 108% on her, ease out to 100% over 1 s | `zoompan` ease-out; kinetic text pops word by word | Soft hit on first word | Hook line (pick one below) |
| 2.9–11.0 | B + C: thing #1 | Stakes / value 1 | Goal gradient | Hard cut to 100%; punch-in to 110% on "Christmas" | Number badge **1/3** slides in | Pop on badge, whoosh on punch-in | **1/3** + {{thing 1}} |
| 11.1–18.7 | D + E: Selfridges windows, traffic-cone tree | Value 2 | Specificity, pattern interrupt | Cut to 110% on him; back to 100% at "traffic cones" | Badge **2/3** | Pop on badge | **2/3** Selfridges windows |
| 18.8–22.1 | F: "the third, the last and the biggest" | Build | Prediction | Slow push 100→110% | `zoompan` slow push | Riser into peak; music drops for 0.3 s at the end | **3/3** … |
| 22.2–24.7 | G: "Harry Potter's biggest store" | **PEAK** (≈ 72%) | Peak-end, payoff | Hard cut to 110%, hold | Big word "HARRY POTTER" slams in (top band) | Hit on "Harry Potter"; music back in | **3/3** Biggest Harry Potter store |
| 24.8–31.0 | I: night bus + "follow for details" | Payoff + CTA | Peak-end, open loop | Cut back to 100% (wide, both of you) | CTA card above the faces in the last 2 s | Small pop on CTA | "Follow for part 2 🚌" |

Hero effects: two at most, ≥ 6 s apart. The 1/3 → 2/3 → 3/3 progress badge carries the list (stands in for `/effects todo`), and the "HARRY POTTER" slam at the peak (stands in for `/effects backdrop-word`).

Captions: 2–4 words, one highlighted key word (yellow), at ~60% frame height (chest), clear of the right-side buttons and the bottom 20%.

Look: lift and warm the faces, pull down the window highlights, gentle vignette so the busy desk falls back.

Sound: voice high-pass, denoise, gentle compression, −14 LUFS / −1 dBTP. One sound owner (my ffmpeg mix). 5 SFX + a quiet light-beat instrumental from **Epidemic Sound** (licensed via your connector), ducked ~18 dB under the voice. Licences logged in `credits.txt`.

## 3 hook lines (from what is said in A)

1. **"Before you go to Oxford Street…"**
2. **"3 things before Oxford Street"**
3. **"Don't do Oxford Street without #3"**

## Peak

**G — "Harry Potter's biggest store"** at ≈ 22 s of 31 s (≈ 72%). Strongest payoff, and it is what F promised ("the last and the biggest").

## Ending — suggestion

The words end on "follow for more details", so a specific CTA fits better than a loop: **"Follow for part 2 — the Harry Potter night bus 🚌"**. A loop would need the last line to lead back into "Before Oxford Street…", which it doesn't.

---

**STOP — waiting for "go"**, plus answers to the 4 questions above (or say "go, use your readings").
