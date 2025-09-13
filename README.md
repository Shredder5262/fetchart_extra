fetchart_extra

A beets
 plugin that extends the built-in fetchart to download and manage extra album artwork: discart (CD art), back covers, and spines.
It checks your filesystem first, then fetches from multiple sources, and applies post-processing so your artwork is consistent, clean, and properly sized.

✨ Features

Artwork types supported:

Discart (CD label art)

Back covers

Spines

Sources:

Fanart.tv

TheAudioDB

MusicBrainz Cover Art Archive

Filesystem check first — skips download if the art already exists.

Multi-disc support — saves multiple discarts as discart1.png, discart2.png, etc.

PNG output normalization — all saved artwork is converted to .png.

Automatic post-processing:

Removes white backgrounds from discart (with multi-corner + center floodfill).

Resizes each artwork type:

Discart → 1000×1000 px

Back → 750×750 px

Spine → 35×700 px

Configurable fuzz tolerance for background removal.

Resilient networking — handles timeouts and SSL errors gracefully.

Logging:

By default, only warnings are shown.

Run with -v to see detailed logs about fetching, saving, resizing, and cleaning.

⚙️ Configuration

Add to your config.yaml:
```yaml
plugins: fetchart_extra

fetchart_extra:
  fanarttv_key: YOUR_FANARTTV_API_KEY
  theaudiodb_key: YOUR_AUDIO_DB_API_KEY
  sources: [fanarttv, theaudiodb, musicbrainz]
  types: [discart, spine, back]
  run_on_import: yes
  resize:
    enabled: yes
    discart: [1000, 1000]
    back: [750, 750]
    spine: [35, 700]
  fuzz: 15%
  background:
    multi_corner: yes
```

sources: Priority order. First source that returns valid art wins.

types: Choose which artwork to fetch.

run_on_import: Automatically fetch on album import.

resize: Dimensions per art type.

fuzz: Tolerance for background removal.

background.multi_corner:

yes → removes background from all four edges + center hole.

no → only removes background from the top-left edge.


📦 Installation

Copy fetchart_extra.py into your beetsplug directory (e.g. /config/beetsplug/).

Enable it in your beets config under plugins.

Add your API keys (Fanart.tv and TheAudioDB).

Run manually or let it process automatically on import.

🚀 Usage
Manual run
```
beet fetchart_extra
```
Pretend mode

See what would happen without downloading:
```
beet fetchart_extra --pretend
```
Verbose logs
```
beet -v fetchart_extra
```

📝 Example Output

With -v:
```
✔ discart ready for BABYMETAL – BABYMETAL (from fanarttv)
✔ back ready for Gotye – Making Mirrors (from musicbrainz)
→ Skipping spine: MusicBrainz does not provide spine images
✔ spine ready for 12 Stones – Picture Perfect (from theaudiodb)
⚠ No valid back found for Artist – Album
```

Without -v:
Only warnings and errors:
```
⚠ No valid back found for Artist – Album
```

📌 Notes

MusicBrainz does not provide spine art; only Fanart.tv and TheAudioDB do.

All output files are saved as .png.

Multi-disc albums → discart1.png, discart2.png, etc.

If a source API fails, the plugin skips to the next source gracefully.

Works alongside beets’ built-in fetchart if you want both, but recommended to use this plugin for discart/back/spine while letting fetchart manage only front covers.

🔧 Troubleshooting

ImageMagick errors
Ensure ImageMagick v7 is installed. If convert is deprecated, use magick in your PATH.

White center hole not removed
Enable background.multi_corner: yes to also floodfill from the disc center.

No results from sources

Verify your API keys are valid.

Try reordering sources in config.

📜 License

MIT
