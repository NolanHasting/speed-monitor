# Speed Monitor

A personal, foreground iPhone GPS speed monitor. No account or API key required for modest personal testing. Not a safety-certified instrument.

## Install
1. Open the published HTTPS site in Safari on iPhone. Use Share > Add to Home Screen (enable Open as Web App if offered).
2. Open the icon while parked. Tap Test sound, confirm it is audible at your intended volume and audio output, and try Demo.
3. Tap Exit demo, then Start drive. Allow location access with Precise Location enabled. Keep the app in the foreground, mounted safely.
4. Stop monitoring when parked. Do not manipulate your phone while driving.

## Behavior
GPS speed is displayed as whole mph and internally rounded to 0.1 mph and compared against an explicit mapped limit. Above the limit turns red and plays three short beeps once per overspeed episode; the alert rearms after two seconds at/below limit. Missing speed, stale or inaccurate GPS, missing/ambiguous mapped limits and certain conditional speed tags produce neutral state rather than green. No default limits are inferred. Map matching uses distance and heading and is heuristic, not navigation-grade. Parallel roads, intersections, temporary limits and missing map data can still lead to incorrect results. Always follow posted signs and your vehicle speedometer.

The app requests a screen wake lock and releases it when stopped. It does not monitor or warn reliably with the screen locked, app backgrounded, or audio interrupted; it is not a native app or CarPlay app. The tone is in-app audio, not an iOS notification. Test actual audio output before use. A demo works without GPS or network after the page loads.

## Hosting
Enable GitHub Pages from the main branch root in Settings > Pages. All assets are relative to the repository path.

## Map service and privacy
Small bounding-box queries use spatially clipped road geometry. Road geometry is retrieved from the public OpenStreetMap Overpass endpoints (Private.coffee first, overpass-api.de fallback) using rounded coordinates for nearby areas, not for every GPS fix. The app caches up to ten areas in memory, throttles requests to normally at most one every 20 seconds, only near the edge of a cached area, with bounded failure backoff, and limits requests to 150 and retrieved data to approximately 12 MB per UTC day per browser (a final response may exceed that byte threshold). Public server limits, network loss and missing map data may make the speed limit unavailable; this implementation is for modest individual testing, not a public production deployment. Production use should use a contracted map matching/speed-limit API or a self-hosted OSM service. No analytics, trip history, or coordinate persistence in the app; only a map usage counter is stored. The map service receives request coordinates and IP address under its own policies. The service worker caches the app shell, not road data.

Map data attribution: © OpenStreetMap contributors, https://www.openstreetmap.org/copyright.
