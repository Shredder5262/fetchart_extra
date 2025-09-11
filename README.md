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
