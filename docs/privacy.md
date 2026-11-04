# Privacy Policy — Steam Revenue Estimate

Last updated: November 4, 2026. Draft for the unpacked extension; a publisher contact and public policy URL must be supplied before store submission.

## Data processed and stored

The extension reads the current Steam game's AppID and public game facts: product eligibility, ordinary US price, review totals and their coverage. It caches up to 200 games locally with acquisition timestamps and stores the user's estimation parameters locally. Cached AppIDs can reveal which Steam games were inspected; the extension does not record general browsing history, titles of other tabs or visits to other websites.

It does not collect Steam account identifiers, credentials, player profiles, review text, reviewer identities, communications, payment information or analytics. Public revenue estimates are calculated on the device.

## Requests to Steam

The extension sends the current AppID and fixed US market to `store.steampowered.com` for pricing, and the current AppID and review-filter parameters to `api.steampowered.com` for review totals. Only the aggregate review summary is used; individual reviews and reviewer details returned by Steam are not stored or used. Requests omit credentials and require no API key. Steam receives the request and standard network information such as the IP address and may process it under [Valve's privacy policy](https://store.steampowered.com/privacy_agreement/).

There is no extension backend or telemetry. The extension does not send its local cache or user settings to the publisher or other analytics services. A manually opened methodology link navigates to the linked external website under normal browser behavior.

## Retention and controls

Settings stay locally until reset or the extension is removed. Reset in the gear settings panel restores the default assumptions. Cache facts are fresh for 24 hours and eligible for fallback for up to seven days; older entries are not used for estimates. Cache entries are overwritten on successful refresh or evicted at the 200-game limit, rather than being automatically deleted on a seven-day schedule. Removing the extension deletes its browser-managed local storage.

Data is not sold, used for unrelated purposes or used for creditworthiness or lending. There is no account, tracking cookie or synchronization of local settings to other devices.

## Changes and contact

This document must be updated if extension behavior changes. Publisher/support contact is pending in CHROMEWEBSTORE.md; this draft must not be presented as a completed store submission policy until those details and a public URL are provided.
