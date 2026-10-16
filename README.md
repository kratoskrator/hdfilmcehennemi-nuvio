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

## Verification

On 16 October 2026, all 30 automated tests passed. Live website checks resolved two sources each for Inception and Interstellar, including five and six subtitles respectively. Their first HLS playlists loaded and each listed two audio renditions.

The live checks supplied known TMDB metadata locally; site search, movie pages, player pages and playlists were fetched live. Actual video playback and TMDB authentication inside Nuvio were not tested. A live series page returned HTTP 403, so live TV extraction remains unverified. Website access and player formats can change.

## Source and development

Download [the complete source package](./hdfilmcehennemi-nuvio-source.zip) for source files, build tools, tests, local hosting and full development instructions. It has no install-time dependencies; Node.js 18 or later is sufficient to build and test it.

The provider in this repository is at the root, and its manifest filename is **hdfilmcehennemi.js**. The source package uses **providers/hdfilmcehennemi.js**; preserve the root filename when replacing the published provider with a rebuilt version.

## Credits

MIT licensed. Decoder behavior and earlier site formats were adapted from [Batuhan4/hdfilmcehennemi-stremio](https://github.com/Batuhan4/hdfilmcehennemi-stremio), maintained from enXov's MIT-licensed integration. See [LICENSE](./LICENSE) and [third-party notices](./THIRD_PARTY_NOTICES.md).

Title matching uses [The Movie Database](https://www.themoviedb.org). This product uses the TMDB API but is not endorsed or certified by TMDB.
