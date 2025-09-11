# fetchart_extra

A beets
 plugin that extends the built-in fetchart to download extra album artwork: discart (CD art), back covers, and spines.

✨ Features

Fetches artwork from multiple sources:

Fanart.tv

TheAudioDB

MusicBrainz Cover Art Archive

Checks the filesystem first before downloading.

Handles multi-disc albums (discart1.png, discart2.png, …).

Normalizes output to PNG.

Automatic post-processing:

Removes white disc backgrounds using ImageMagick.

Resizes to configurable dimensions:

discart → 1000×1000

back → 750×750

spine → 35×700

Configurable fuzz tolerance for background removal.

Resilient networking: skips gracefully on timeouts or SSL issues.

Verbose logs: shows which source provided each artwork.

plugins: fetchart_extra

# fetchart_extra:
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


✔ discart ready for BABYMETAL – BABYMETAL (from fanarttv)
✔ back ready for Gotye – Making Mirrors (from musicbrainz)
→ Skipping spine: MusicBrainz does not provide spine images
✔ spine ready for 12 Stones – Picture Perfect (from theaudiodb)
⚠ No valid back found for Artist – Album


📦 Installation

Copy fetchart_extra.py into your beetsplug directory (e.g. /config/beetsplug/).

Enable it in your beets config under plugins.

Configure API keys (Fanart.tv and TheAudioDB).

Run beet fetchart_extra or let it run automatically during imports.

📌 Notes

MusicBrainz does not provide spine art. Only Fanart.tv and TheAudioDB do.

All artwork is saved in PNG format regardless of source.

Multi-disc albums create discart1.png, discart2.png, etc.

If a source API fails, the plugin skips gracefully and tries the next.
