# Creative Similarity Scanner

Client-side tool that estimates which of a set of ad creatives Meta's retrieval
stage would collapse into a single Entity ID, and which signal is driving it.

Four streams are scored and blended (weights rescale when a stream is missing):

| Stream | Weight | Source |
| --- | --- | --- |
| Visual | 35% | dHash structure signature + 4x4 colour signature, over 5 sampled video frames |
| Text   | 25% | pasted ad copy — term cosine + bigram Jaccard |
| Theme  | 25% | manual tags: persona, benefit, awareness, format |
| Audio  | 15% | 8-band FFT profile, spectral centroid, silence ratio, dynamics |

Assets above the collapse threshold are clustered (average linkage), and one
representative per cluster is recommended for upload.

## Notes

- Everything runs in the browser. No file is ever uploaded anywhere.
- The session is kept in IndexedDB per browser, so a reload keeps your work.
- The threshold is our setting. Meta has never published a number, and this is
  an estimate rather than a reimplementation of their model.

## Development

Static single file. Open `index.html`, or serve the directory with any static
server. No build step, no dependencies.
