# Motion verification

Method: extract frames 1 s apart, convert to grayscale at 320x180, compute the
mean absolute pixel difference between consecutive frames (0–255 scale).
A near-static clip scores < 5; a clip with real subject/camera motion scores
well above 15 on every step. Frames were also read visually.

## Source clips (each 1280x720, 24 fps, 10.0 s)

| Clip | Scene | Mean diff / 1 s step | Min step | Max step | Visual check |
|---|---|---|---|---|---|
| 1 — prediction auction | Robot agents crowd a neon prediction marketplace, waving bid paddles; price boards flip overhead, papers fly; camera sweeps through the crowd to the live auction stage | 34.61 | 31.11 | 38.08 | t=0: robot crowd at market stalls under chart screens. t=5: completely different angle — the LIVE AUCTION stage, auctioneer with gavel, price boards reading PRICE +124, papers mid-air. Real subject + camera motion. |
| 2 — courtroom verdict | Robot defendant in the dock as a judge robot slams a glowing gavel; evidence screens flash VERDICT: GUILTY and CASE CLOSED; camera dollies down the aisle to the bench | 40.42 | 30.29 | 50.39 | t=0: defendant robot facing the bench, papers flying, judge in the distance. t=5: close-up of the judge robot slamming the glowing gavel, VERDICT: GUILTY screens behind. Real subject + camera motion. |
| 3 — rocket launch | Rocket blasting off at dawn, flames and smoke billowing; camera tracks upward alongside it past a giant glowing leaderboard tower | 30.38 | 20.65 | 45.80 | t=0: rocket on the pad, engines firing, smoke billowing. t=5: rocket high in the sky beside the leaderboard tower, long flame trail, sparks falling. Real subject + camera motion. |

Per-second step values:

- Clip 1: 38.08, 37.05, 35.68, 35.78, 36.09, 33.37, 31.68, 31.11, 32.70
- Clip 2: 30.29, 40.25, 40.23, 33.91, 39.22, 44.30, 50.39, 47.74, 37.44
- Clip 3: 45.80, 38.33, 35.25, 32.00, 28.95, 28.02, 22.87, 21.51, 20.65

All three clips PASS: no step below 20.65, no static segment.

## Final video — `aiprove-w6-explainer.mp4`

- ffprobe: 60.000 s, 1280x720, H.264 + AAC, 38,052,004 bytes (~36.3 MB)
- 60 frames extracted at 1 fps; mean per-second diff **35.48** overall.
- Every non-end-card step is ≥ 20.59. The only near-zero steps are t=55–59 s:
  the static end card (55–60 s), which is a title card by design, not footage.
  The cut into the end card registers as 97.75.
- Timeline: clip 1 x2 (0–20 s), clip 2 x2 (20–40 s), clip 3 + first 5 s of
  clip 3 (40–55 s), end card (55–60 s). Narration runs 0.3–55.0 s
  (volumedetect: mean −21.5 dB in 0–10 s, −20.6 dB in 25–35 s, −21.4 dB in
  50–55 s; −91.0 dB in the 55–60 s end-card window, i.e. silence by design).
- Visual spot checks (accurate seek): t=5 s live auction stage with price
  boards; t=25 s judge robot slamming the glowing gavel, VERDICT: GUILTY;
  t=45 s rocket climbing past the leaderboard tower; t=57 s end card reading
  "AIProve — Free to enter · Graded in the open · Paid in stock — Join now:
  aiprove.fun/r/4d6a7885 — Entry by RapidPilot2".
- No other identity's handle, referral code, wallet, or GitHub name appears
  anywhere in the video, narration, end card, or repo files — only
  RapidPilot2 / 4d6a7885 / raisya0007.
