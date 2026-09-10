# MASTER EXECUTION PROMPT — MINNESOTA NORTHERN LIGHTS LIVE

Build and release **Minnesota Northern Lights Live** end to end as an independent Vercel/GitHub product. The Michigan Northern Lights implementation is a reference only: do not edit `izworskic/chrisizworski-com`, `/northern-lights-michigan/`, Michigan `/api/aurora`, Michigan parser files, routing, canonical metadata, or make Michigan depend on this repository. Any Michigan write is a -100 hard veto and blocks release.

## Decision
Within the first viewport answer: **Is it worth going out tonight in Minnesota, where should I go, when is the best window, and what could ruin the view?** Show a plain-language verdict, a clearly labeled 0–100 Viewing Score, selected Minnesota region, NOAA OVATION signal, NWS cloud context, peak 24-hour Kp, best dark window, and three-night outlook. The score is a planning index, never a sighting probability and never shown with a `%` sign.

## Data
Use primary public sources: NOAA SWPC planetary Kp forecast/current Kp, NOAA OVATION Aurora 30-Minute Forecast, NOAA real-time solar-wind magnetic field and speed, NWS API sky cover/hourly day-night data, and USNO moon phase/illumination. Use `Promise.allSettled`/soft failure. Missing values stay null. Never convert missing values to zero. Never call Kp or OVATION a local probability. Suppress the numeric score without useful darkness, and do not create a numeric score when both Kp and OVATION are unavailable.

## State model
`config/state.js` is authoritative. Include Voyageurs/International Falls, Ely/Boundary Waters, Grand Marais/Gunflint, Bemidji/north-central Minnesota, Duluth/North Shore, and Twin Cities/southern Minnesota. Each region needs id, label, places, latitude, longitude, and an approximate planning Kp threshold. Planning Kp is a travel/monitoring threshold, not a physical visibility boundary.

## Score
OVATION up to 40; Kp relative to regional threshold up to 25; NWS clouds up to 20; darkness 8; southward Bz up to 4; solar-wind speed up to 3; very bright moon penalty up to 5. Clamp 0–100. Labels: 70–100 Strong viewing setup; 50–69 Possible — worth checking; 30–49 Watch conditions; 0–29 Unlikely right now; high clouds plus meaningful signal = Aurora signal, poor sky; no darkness = No useful darkness; Kp + OVATION missing = Live space-weather unavailable.

## UX
Emulate the successful Michigan editorial experience without copying Michigan text: light paper shell, restrained green typography, dark aurora hero, circular score gauge, region selector, three decision factors, three-night strip, current Kp/solar wind/moon cards, Minnesota regional outlook, truth/source section, and mobile-first layout. Keep technical explanation below the decision layer.

## SEO
Canonical `https://chrisizworski.com/national-tools/aurora/minnesota/`. Unique title/description, WebApplication and BreadcrumbList schema, index/follow page, API `X-Robots-Tag: noindex, nofollow`, state-specific content sufficient to avoid doorway/thin-page behavior. Target northern lights Minnesota tonight, aurora forecast Minnesota, can I see northern lights in Minnesota, northern lights Voyageurs/Boundary Waters/North Shore, aurora borealis Minnesota, best place to see northern lights in Minnesota.

## Reliability
Static HTML under 150 KB. API `s-maxage=300, stale-while-revalidate=900`, ~8 s upstream timeout, no paid data, no DB, no Replit runtime, independent Vercel deployment.

## Tests
Test NOAA header-row Kp parsing, OVATION longitude normalization, sky-cover intervals, null preservation, score clamps, no score without darkness, no score with Kp+OVATION unavailable, unique valid region ids/coordinates/default region, correct canonical, score not formatted as percent, and API noindex header.

## Value function — release target >=92/100
Decision clarity 20; data reliability/truthfulness 20; Minnesota specificity 15; repeat-visit value 10; mobile/accessibility 10; performance/resilience 10; SEO 10; source transparency 5.

## Loss function
Michigan write -100; false sighting probability -50; missing data→zero -40; broken region selector/API -35; stale data as live -35; generic state clone -25; failed tests/build -25; bad canonical -25; weak mobile first-view -20.

Execute research, implementation, tests, build validation, Git commit, Vercel deployment, smoke tests, canonical/API-header verification, then re-check Michigan SHA. Only after passing should the National Tools hub link be added, without modifying Michigan aurora behavior.
