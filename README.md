# HDFilmCehennemi for Nuvio

A movie and TV playback provider for Nuvio, using hdfilmcehennemi.nl.

## Install

In Nuvio, open **Settings → Plugins**, add the following manifest address, refresh and enable **HDFilmCehennemi**. Menu names can vary by app version.

```text
https://raw.githubusercontent.com/kratoskrator/hdfilmcehennemi-nuvio/main/manifest.json
```

This provider adds playback sources for titles selected in Nuvio. It does not import the website's homepage or browsing categories as a catalog.

## Features

- Movie lookup by IMDb identifier, with exact-title fallback.
- Season and episode selection for TV titles.
- Alternative players, current salt-derived decoders, and available subtitles.
- Original HLS masters, preserving their available audio languages.
- A self-contained provider without external runtime dependencies or execution of downloaded page scripts.

The provider uses Nuvio's supplied TMDB key when available. If your build does not provide one, enter your own TMDB API key or API Read Access Token in provider settings. [TMDB authentication documentation](https://developer.themoviedb.org/docs/authentication-application).

## Version 1.0.1

- Sends the actual search, series and episode referrer when following pages and loading players.
- Uses document/AJAX Accept headers and retries temporary GET transport errors or HTTP 502/503/504 once.
- Shares a 45-second lookup deadline; in-flight requests on TV builds without guest timers still rely on Nuvio's native timeout.
- Stops repeated requests to an origin after HTTP 403/429/451 or a recognized verification response.
- Enforces the TV's 1 MiB UTF-8 response limit. No manual site-cookie forwarding or downloaded-script execution.

Refresh this repository in Nuvio to obtain the update. The manifest address is unchanged.

## Verification

On 16 October 2026, all **51 automated tests** and **nine Nuvio TV QuickJS engine checks** passed. Engine checks used Nuvio's exact polyfill with 32 MiB memory and 512 KiB stack, covering movie/episode resolution, stored real players, referrers, access blocks and bounded retries.

Live checks of the updated bundle through the official Nuvio TV networking service running on Windows Node returned two Inception sources. Breaking Bad search succeeded, but the series page still returned **Cloudflare HTTP 403**. **This update does not resolve that demonstrated access restriction.**

Live checks supplied known TMDB metadata locally; website requests were live. Physical Samsung TV playback and TMDB authentication inside Nuvio were not tested. The plugin runs directly in Nuvio and does not add a PC resolver. Website access and player formats can change.

## Source and development

Download [the complete source package](./hdfilmcehennemi-nuvio-source.zip) for source files, build tools, tests, local hosting and full development instructions. It has no install-time dependencies; Node.js 18 or later is sufficient to build and test it.

The provider in this repository is at the root, and its manifest filename is **hdfilmcehennemi.js**. The source package uses **providers/hdfilmcehennemi.js**; preserve the root filename when replacing the published provider with a rebuilt version.

## Credits

MIT licensed. Decoder behavior and earlier site formats were adapted from [Batuhan4/hdfilmcehennemi-stremio](https://github.com/Batuhan4/hdfilmcehennemi-stremio), maintained from enXov's MIT-licensed integration. See [LICENSE](./LICENSE) and [third-party notices](./THIRD_PARTY_NOTICES.md).

Title matching uses [The Movie Database](https://www.themoviedb.org). This product uses the TMDB API but is not endorsed or certified by TMDB.
