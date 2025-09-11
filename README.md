#fetchart_extra

A beets
 plugin that extends the built-in fetchart functionality to download additional album artwork types: discart (CD art), back covers, and spines.

✨ Features

Fetches discart, back covers, and spines from multiple online sources

Fanart.tv

TheAudioDB

MusicBrainz Cover Art Archive

Checks your local filesystem first before downloading (avoids duplicates).

Handles multi-disc albums: saves discart.png or discart1.png, discart2.png, etc.

Normalizes all output images to PNG.

Automatically:

Removes white backgrounds from discart using ImageMagick (magick).

Resizes images to configurable defaults:

discart → 1000×1000

back → 750×750

spine → 35×700

Configurable fuzz factor for background removal.

Robust error handling: skips gracefully if a source API is unavailable or returns invalid data.

Detailed logging: shows which source provided each artwork.

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


✔ discart ready for BABYMETAL – BABYMETAL (from fanarttv)
✔ back ready for Gotye – Making Mirrors (from musicbrainz)
→ Skipping spine: MusicBrainz does not provide spine images
✔ spine ready for 12 Stones – Picture Perfect (from theaudiodb)


📦 Installation

Drop fetchart_extra.py into your beetsplug directory (e.g. /config/beetsplug/) and enable it in your beets config under plugins:.
