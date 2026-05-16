# NoMercy Media

Static media-asset repository for the NoMercy player ecosystem. Serves as a
CORS-friendly content origin for the testbed, the examples site, and any
third-party demo that needs working playlists.

All content here is either Creative Commons-licensed (films, music) or used
as test material under the original rights holders' copyright (anime).

> **Rights holders:** see [Takedown policy](#takedown-policy) below.

---

## At a glance

| Folder    | Contents                                            | License model                                            |
|-----------|-----------------------------------------------------|----------------------------------------------------------|
| `Films/`  | 16 Blender open movies (2006–2023)                  | CC BY 2.5 / 3.0 / 4.0                                    |
| `Music/`  | 9 Free Music Archive albums                         | CC0 / CC BY / CC BY-NC-SA / CC BY-ND (per-album)         |
| `Anime/`  | 2 test episodes — ASS subtitle + embedded-font fixtures | All rights reserved (test content only)               |
| `Fonts/`  | Subtitle fonts referenced by Anime ASS files        | Per-font (see `fonts.json` inside each show)             |

Each section has a root `ATTRIBUTION.md` + `ATTRIBUTION.json`, plus per-item
`ATTRIBUTION.md` + `.json` inside each film / album / show folder.

---

## URL pattern

Consumers fetch over `raw.githubusercontent.com`:

```
https://raw.githubusercontent.com/NoMercy-Entertainment/nomercy-media/master/<Section>/<Item>/<File>
```

Example — Cosmos Laundromat master playlist:

```
https://raw.githubusercontent.com/NoMercy-Entertainment/nomercy-media/master/Films/Cosmos.Laundromat.(2015)/Cosmos.Laundromat.(2015).NoMercy.m3u8
```

CORS is permissive (GitHub raw sets `Access-Control-Allow-Origin: *`), so the
content works directly from a browser without a proxy.

---

## Folder conventions

### Films

```
Films/
└── <Title>.(<Year>)/
    ├── <Title>.(<Year>).NoMercy.m3u8     ← HLS master playlist
    ├── audio_<lang>_<codec>/             ← audio rendition group
    ├── video_<W>x<H>[_SDR]/              ← per-tier HEVC HDR/SDR ladder
    ├── subtitles/                        ← WebVTT per language
    ├── thumbs_<W>x<H>.vtt + .webp        ← sprite preview thumbnails
    ├── fonts/ + fonts.json               ← embedded subtitle fonts (if any)
    ├── luts/ + luts.json                 ← color-grading LUTs (if any)
    └── ATTRIBUTION.md + .json
```

### Music (MusicBrainz Picard-style layout)

```
Music/
└── <Letter>/<ArtistName>/
    ├── <ArtistName>.png                  ← artist image
    └── [<Year>] <AlbumTitle>/
        ├── cover.jpg
        ├── <NN> <TrackTitle>.mp3
        ├── <NN> <TrackTitle>.jpg         ← per-track artwork
        └── ATTRIBUTION.md + .json
```

ID3v2 tags on every MP3 are normalised to canonical Free Music Archive
values (title, artist, album, track number, year). Audio bitstream is not
re-encoded.

### Anime

```
Anime/
└── <Show>.(<Year>)/
    └── <Show>.S<season>E<episode>/
        ├── <Show>.(<Year>).S<season>E<episode>.NoMercy.m3u8
        ├── audio_<lang>_<codec>/
        ├── video_<W>x<H>/
        ├── subtitles/                    ← ASS / SSA test fixtures
        ├── fonts/ + fonts.json
        └── ATTRIBUTION.md + .json
```

---

## License overview

### Films

| Era       | License    | Examples                                                                                                              |
|-----------|------------|-----------------------------------------------------------------------------------------------------------------------|
| 2006      | CC BY 2.5  | Elephants Dream                                                                                                       |
| 2008–2016 | CC BY 3.0  | Big Buck Bunny, Sintel, Tears of Steel, Cosmos Laundromat, Caminandes (1–3), Glass Half            |
| 2017–2023 | CC BY 4.0  | Agent 327, The Daily Dweebs, HERO, Spring, Coffee Run, Charge, Wing It!                                               |

### Music

| License            | Album count                                       |
|--------------------|---------------------------------------------------|
| CC0 1.0            | 1 (HoliznaCC0 — Power Pop!)                       |
| CC BY 4.0          | 3                                                 |
| CC BY-NC-SA 3.0    | 1 (The Kyoto Connection — Wake Up)                |
| CC BY-NC-SA 4.0    | 1 (Derek Clegg — KJC)                             |
| CC BY-ND 4.0       | 1 (bent wyre)                                     |
| Mixed per-track    | 2 (legacyAlli, Mr Smith — see per-album ATTRIBUTION) |

### Anime

Commercial copyrighted works (Silver Link, Passione). Hosted as test
fixtures for the player's ASS subtitle + embedded-font handling. Not
distributed under a permissive license. See [Takedown policy](#takedown-policy).

---

## Attribution

Every consumer of this content is required to provide attribution per the
applicable Creative Commons license. The format follows the CC TASL pattern
(Title, Author, Source, License).

Detailed per-item attribution lives at:

- `Films/ATTRIBUTION.md` (root index) and `Films/<Film>/ATTRIBUTION.md` (per-film)
- `Music/ATTRIBUTION.md` (root index) and `Music/<Letter>/<Artist>/[<Year>] <Album>/ATTRIBUTION.md` (per-album)
- `Anime/ATTRIBUTION.md` (root index) and `Anime/<Show>/ATTRIBUTION.md` (per-show)

JSON equivalents (`ATTRIBUTION.json`) exist at every path for programmatic
consumption.

---

## Modifications notice

Per CC BY: derivative works must indicate what changed. NoMercy modifications
to upstream Blender / Free Music Archive content include:

- **Video** — transcoded to HLS with custom HEVC ladder (`hvc1.2.4`), both
  HDR (PQ) and SDR variants; sprite-VTT preview thumbnails generated;
  embedded subtitles re-muxed as standalone WebVTT; embedded fonts and
  color-grading LUTs extracted to separate sibling manifests.
- **Audio** — bitstream preserved bit-for-bit; only ID3v2 tags normalised to
  canonical Free Music Archive titles and licensing.
- **Anime** — same video pipeline; ASS subtitles preserved as authored;
  embedded fonts extracted to `fonts/` so cross-platform players can load
  them without container parsing.

The original works are unchanged at the artistic level. All modifications
are mechanical / packaging-level only.

---

## Takedown policy

If you are a rights holder and want content removed, open an issue on this
repository **or** email `takedown@nomercy.tv` with:

1. The URL of the content
2. Proof of rights (or a verifiable identity link)
3. Whether you want the content removed entirely or replaced with a marker
   that points at the official source

Content is removed within 7 days of a verified request — no questions asked,
no counter-claim process, no friction. The intent of this repository is to
provide CC-friendly test material; nothing here is worth a fight.

---

## Related repositories

- [`nomercy-player-kit`](https://github.com/NoMercy-Entertainment/nomercy-player-kit) — headless contract substrate (28 adapter ports)
- [`nomercy-video-player`](https://github.com/NoMercy-Entertainment/nomercy-video-player) — reference video adapter (v2 on `feature/api-unification-consolidation`)
- [`nomercy-music-player`](https://github.com/NoMercy-Entertainment/nomercy-music-player) — reference music adapter (v2 on `feature/api-unification-consolidation`)
- [`nomercy-workspace`](https://github.com/NoMercy-Entertainment/nomercy-workspace) — monorepo containing the testbed and examples site
