# Speed Monitor

A personal foreground iPhone GPS speed monitor using TomTom Snap to Roads. No navigation destination required.

## Setup
1. Create an account at https://my.tomtom.com/ and create an API key with Snap to Roads (TomTom Maps, not Orbis preview) access.
2. Restrict the key to the website origin if supported and set account-side spending/usage limits. Never commit a key to this repository.
3. Open the HTTPS app in Safari, add to Home Screen, and open Set up TomTom road data while parked. Save your key in the app. The key is stored in local browser storage, not on a server or in the repository; browser storage is not a secure secret vault.
4. Use Test connection in the TomTom setup panel to check the key against public example coordinates (one API request), then test sound and Start drive, allow Precise Location and keep the app visible. TomTom requires at least two distinct real GPS positions; no location is fabricated. GPS speed is available without a key, but automatic limits are not.
5. Observe posted signs and your vehicle speedometer. Do not interact with the phone while driving.

## How it works
The request uses measurementSystem=auto and a 30-meter offroadMargin. The app sends a short rolling GPS trace to TomTom's map-matching API, looks up the speed limit on the road element referenced by the last projected point, checks match confidence and snap distance, converts speed units, and compares GPS speed with the returned maximum. Unmatched or stale positions, missing limits, uncertain direction, and network failures remain neutral. Map data can still be wrong and may not reflect temporary, school-zone, or variable limits.

Requests are throttled to one per five seconds, with backoff on errors and a local 2,300-request-per-calendar-month cap per browser. The cap is not an account-wide billing guarantee; TomTom pricing and transaction accounting apply. The free evaluation is for limited testing; continuous driving may require paid service. See https://docs.tomtom.com/pricing. The app retains no trip history; a small recent trace is held in memory and sent to TomTom, which receives coordinates, timestamps, API key and IP address. The key and usage count are stored locally. No analytics. The app does not reliably monitor when backgrounded or locked.

## Source
TomTom Snap to Roads API: https://docs.tomtom.com/snap-to-roads-api/documentation/snap-to-roads-api/synchronous-snap-to-roads

GitHub Pages serves the static app shell. The provider must be configured on each browser/device. Map data © TomTom.
