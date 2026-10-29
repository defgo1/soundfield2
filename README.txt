SOUNDFIELD V2.0 — DECENTRALISED SONIC EVENT REHEARSAL
========================================================

PACKAGE
index.html, sw.js, manifest.webmanifest, icon-192.png, icon-512.png

WHAT'S NEW
- Keeps the original 96 BPM musical programme as an option.
- Adds 64-second experimental event study: sync beacons, pulsed notes, sustained drones, sweeps and silence.
- Editable and shareable JSON score, preloaded on each phone from an invitation link.
- 2x2, 3x3 or 4x4 grid for 40m, 80m, 120m or 200m square stages.
- Musical part assigned by device number, repeating every five devices.
- Per-device audio timing adjustment (default 0ms; change only after measuring real offsets).
- Elapsed-time counter and local diagnostics; copy individual reports for comparison.
- Attempts to hold the screen awake; detects visibility and audio interruptions.

INSTALL / UPDATE ON GITHUB PAGES
1. In the repository containing the original Soundfield, replace index.html,
   sw.js and manifest.webmanifest with the files in this ZIP. Upload icon files too.
2. Settings > Pages > Deploy from branch; ensure branch and folder are correct.
3. Load the HTTPS GitHub Pages URL, and make sure the header says "experimental v2.0".
   If you still see v1, reload after deployment. A previous service worker may
   initially serve cached v1 until the update is installed. Close/relaunch if needed.
4. Each phone visits the HTTPS site directly in Safari or Chrome, not inside an
   in-app preview (some previews block location or audio).
5. When updating the score, send a NEW invitation link to all devices.

HOW TO RUN A 2, 5, 10 OR 20 PHONE TRIAL
1. Choose 80x80m, begin with 2x2 zones and manual mode indoors.
2. Choose Sonic event study. Tap "Begin in 90 seconds" on the host.
3. Copy the invitation link and open it on every device.
4. Assign device numbers 1,2,...,20. The five sonic parts repeat automatically.
5. On EVERY phone, tap "Arm sound & join the piece" (autoplay is restricted).
6. Use each phone's native volume controls. Avoid connecting headphones for acoustic tests.
7. Listen for a shared beep at 0s, 28s and 60s of every 64-second cycle.
8. Record all phone speakers with ONE recording device if you need quantitative
   inter-device acoustic timing. Compare transient onsets on the recording.
9. Use "Copy report" on each phone to collate any visibility interruptions,
   GPS failures, audio state and missed scheduling calls.
10. Repeat for 4x4 on an 80x80m stage only after confirming GPS stability.
    Each cell would be 20x20m. GPS error near boundaries remains a concern.

CHANGING THE COMPOSITION
- Open "Show score JSON" and edit events. All times are seconds into a repeating
  cycle. Valid event types: beacon, pulse, drone, sweep, rest.
- Event fields:
  {"t":4,"type":"pulse","label":"Four short notes","count":4,"gap":0.5}
  {"t":12,"type":"drone","label":"Long chord","duration":6}
  {"t":20,"type":"sweep","label":"Upward pitch glide","duration":3}
  {"t":50,"type":"sweep","label":"Downward pitch glide","duration":4,"down":true}
  {"t":60,"type":"beacon","label":"Sync marker"}
  {"t":57,"type":"rest","label":"Silence"}
- Tap "Apply score locally", then "Copy invitation link" to distribute the same
  score to the other devices. The custom score is encoded in that link, with
  identical hash IDs shown in the app for checking.
- Song changes are NOT broadcast automatically (that would add central/network
  dependence). A different custom score on one phone sounds different.
- After editing a score during playback, a few already scheduled notes may play
  from the previous score. Prefer making edits before arming the devices.

TIMING / LIMITATIONS
- Browser UI counters can vary substantially even when scheduled audio is close.
  Use simultaneous beacon recording, not display differences, to assess sync.
- Phone time settings, audio output latency, CPU scheduling and power management
  can cause audible differences. Timing trim affects sound scheduling, not time.
- There is NO central participant counter, location feed, audio mix, server
  clock calibration or network telemetry. Use device numbers and manual reports.
- The Screen Wake Lock API is best effort, supported unevenly; iOS/Android may
  suspend audio and GPS when locked or app backgrounded. The user must return
  to the app and tap the main audio button again if suspended.
- Phone GPS: requires HTTPS, per-site permission, device location enabled, and
  on some devices 'Precise location' enabled. Avoid in-app browsers/previews.
- GPS smoothing and ~3-4m zone hysteresis help with jitter but cannot create
  precision that the underlying GPS receiver doesn't have.
- GPS position stays in browser JS memory and is not uploaded by this app.
  Stage centre coordinates ARE included in the invitation link and are thus
  visible to its recipients and to the web host handling the initial request.
- Offline caching starts only AFTER successfully loading the site over HTTPS.
- There are no accounts or third-party JS libraries; no analytics.

TESTING NOTES
- JavaScript syntax checked, and automated DOM/scheduler/share-data tests run
  with simulated browser interfaces. This is not a substitute for real-device
  Safari/Chrome testing or a 10-20-device field rehearsal.

TROUBLESHOOTING
- No sound: turn up media volume, switch off silent/playback restrictions where
  applicable, keep screen unlocked, tap Arm once per phone.
- GPS denied: open the actual HTTPS URL in Safari/Chrome; check browser site
  permissions, phone system Location Services, and precise-location setting.
- Wrong zone: ensure all phones use the same invitation link (stage centre,
  size, grid density and shared start timestamp), and check GPS fix accuracy.
- Wrong score: ensure all phones show matching programme and score ID.
- Old version: refresh after uploading the new files; a service worker can
  briefly serve the previous version during an update.
