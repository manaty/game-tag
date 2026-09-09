# Tag 1.0.2 acceptance evidence

The implementing agent ran the following automated checks locally. This is disclosed implementation-agent evidence, not an independent human review or a physical eight-phone network test.

## Engine and sandbox

`npm test`: 13 tests cover capped/randomized rosters, fixed-ring joystick normalization, invalid inputs, spectator rejection, movement/release/300 ms expiry, buffered and double jumps, solid collisions, jump-through and drop-through platforms, springs, speed pads, contact transfer and grace periods, wall occlusion, timer scoring, arena rotation, complete 2- and 8-player matches, ties, save/restore and host time-up. The compiled package is exercised in the real QuickJS sandbox with eight simultaneous input streams over 400 updates; snapshots remain below 20 KB and runtime calls stay within the SDK's enforced budgets.

## Browser and actual host

`npm run test:browser`: two suites.

1. EN/FR/TL layouts with eight players in a sandboxed game iframe: 360×540 phone and 1280×620 display. Joystick, jump, drop-through and result/replay controls fit; horizontal overflow is checked. Sound/music toggles emit persistent host preferences. Reduced motion is enabled. Screenshots show all three arenas and phone layouts.
2. Real SDK HTTP/WebSocket host, shared display and eight isolated browser controller contexts. Checks the actual joystick and simultaneous jump button, pointer release, pause/resume, tag transfer, disconnected-phone behaviour, a complete live 30-second round, results, phone replay and refreshed roster. A late arrival spectates until the next replay. Shared and unique victory paths and organiser end are also exercised.

The contact check uses a saved-state fixture that places two runners together before resuming real QuickJS physics. Later tie/unique-win checks shorten a saved deadline and set scores; they test the real host-to-view result/replay paths. The first 30-second round runs to its natural deadline. Unit tests also simulate complete matches without changing their deadlines. Screenshots with named participants are test fixtures, not real visitor records.

## Limits and deployment checks

Headless Edge/Chromium browser tests do not reproduce every phone, smart TV, packet-loss pattern or audio output device. The renderer bounds extrapolation to 80 ms and the engine ignores expired movement, but subjective latency on a venue's Wi-Fi still needs a real group trial. Visual/sound-toggle checks do not constitute human listening tests. Tagalog is supplied and rendered but has not had an independent native-speaker language review.

The game carries no third-party art or audio. Canvas/SVG scenes and Web Audio synthesis are bundled in the portable package; gameplay does not need a CDN. SDK-supplied player avatars remain host-managed. Public acceptance evidence is tied to the exact package hash and source commit at submission.

Version 1.0.1 skips collision scans for stationary grounded runners, retaining input expiry, buffered jumps and speed-pad refresh. This reduces idle validation/hosting load without changing the 60 Hz physics cadence or sandbox limits.

Version 1.0.2 verifies the tagged-player badge is refreshed when leaving the lobby, even if the initial tagger matches the preview.
