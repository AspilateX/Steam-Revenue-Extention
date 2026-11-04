# Verification — 1.0.2

Checked November 4, 2026 on Windows with Node 24.19.0.

- Confirmed the regression: the old `/appreviews/<appid>` endpoint returns HTTP 302 to the Steam homepage, while product metadata still works.
- Migrated to the documented `IUserReviewsService/GetAppReviews/v1/` endpoint using `input_json`, numeric filter enums, `languages: ["all"]`, Steam purchases, all review types and `filter_offtopic_activity: false`. The parser reads `response.query_summary.total_reviews`; an API key is not required. Existing cache coverage and settings remain compatible.
- `npm run check` passed: strict TypeScript, 82 unit tests, 12 unpacked-extension browser tests, production build and ZIP. New tests cover the real response envelope, request coverage, malformed/retired payloads, and service-worker HTTP requests followed by a cached reload.
- `node scripts/live-smoke.mjs` passed all five live cases in a fresh Chromium profile with no network mocks: Stardew Valley in English/Russian, Terraria, Dota 2 (F2P excluded), and Stellaris: Utopia (DLC excluded). All had correct placement and spacing, with no page errors. Stardew Valley used 902,742 reviews and a USD 14.99 list price; Terraria used 1,248,651 reviews and USD 9.99. English details and the Russian page were visually inspected.
- Manifest V3 remains limited to local storage and the two Steam hosts: Store for product information and API for review totals. ZIP contains only the manifest, bundled background/content scripts and license. Local reports/screenshots remain under ignored `.cache/live-smoke`.

The following records describe earlier releases.

# Verification — 1.0.1

Checked October 7, 2026 with Node 24.19.0 on Windows and Playwright Chromium 153.0.8010.12.

## Automated checks

- TypeScript strict check passed. Main amounts use full USD values rounded to dollars; min–max uses compact USD notation; the title and ranges use 12px text, labels 13px and primary amounts 18px.
- Vitest: 72 tests passed in five files, including the reference homepage result to cents, all multiplier boundaries, additive deductions, settings migration, invalid totals, input validation, cache/retry behavior and UI controls.
- Playwright: eleven unpacked-extension browser tests passed. They cover English/Russian rendering, gear settings, publisher without a recognized link, later metadata above the block without refetching, save/reset without refetch, keyboard details, full billion-dollar amounts fitting 366px and 280px English/Russian columns, missing data, late DOM/navigation, remount, offline fallback, unsupported products, age gates and cache after a browser/worker restart.
- Production build and ZIP passed. Manifest V3, only storage and Steam Store host access; executable code and assets are bundled locally.
- OpenSpec strict validation passed.

## Reference calculation

The reference's public calculator module `/build/_shared/chunk-X7FILJOW.js` was inspected on October 7, 2026. It selects the multiplier from review-count tiers, subtracts 9% regional pricing, 20% discounts and 12% refunds from gross, then subtracts 30% Steam and 20% taxes from the same remaining balance.

Its homepage example (1,540 reviews, $14.99) is reproduced: gross $831,045.60; net $245,158.45; each deduction matches to cents. This verifies formula compatibility given the same inputs, not revenue accuracy against developer accounts.

## Live Steam checks

For version 1.0.0, a fresh Chromium profile ran the production unpacked build with actual Steam requests and no fetch mocks.

| Page | Result |
|---|---|
| Stardew Valley, English | Estimated; USD list price used independently of current discount |
| Stardew Valley, Russian | Estimated; Russian UI and persisted cache |
| Terraria, English | Estimated; concise details and settings visually inspected |
| Dota 2 | Unsupported F2P |
| Stellaris: Utopia | Unsupported DLC |

All five pages passed placement and spacing checks: one block as the last child of the primary metadata container, below publisher and before tags, 14px above its panel and 8px inset from the right edge. Steam overrides outer element padding, so vertical spacing is applied to an inner Shadow DOM frame. Screenshots of the collapsed block, expanded breakdown and Russian settings were visually inspected. Reports and screenshots are ignored artifacts under `.cache/live-smoke`.

## Limits

Steam and the reference may have different review counts, update times or prices. Matching coefficients cannot guarantee identical figures without identical inputs. The model's financial deductions remain assumptions. Store endpoints and DOM can change. No age gate was bypassed and no Steam account was accessed.

Chrome Web Store publication remains outside this change; store assets, public privacy URL and publisher/support information are still needed before submission.
