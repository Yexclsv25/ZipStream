# ZipStream

**Download what's inside an archive — not the archive.**

Paste a link to a ZIP, RAR or ISO. ZipStream reads only the archive's index over the network, then
downloads and unpacks each file straight into `Download/ZipStream/<name>/`. The archive itself never touches
your storage, so a phone that can't hold "zip + extracted files" can still get the files.

## Features
- ZIP / ZIP64, stored RAR (incl. `.part1.rar` sets) and ISO 9660 streaming
- Queue several links, run up to 4 archives at once, retry / cancel each
- Built-in link resolvers: **Pixeldrain**, **MediaFire**, **Buzzheavier**
- Parallel connections, resume for stored files, skip already-downloaded files
- Avoid-rate-limits mode (fewer connections + automatic back-off), Wi-Fi only
- Name filter (only download e.g. `.rpf`), custom headers for cookie/token links
- Share links to the app from any browser
- Native C++ core, Material 3 UI, light/dark

## How it works
1. `Range` request for the end of the file → C++ finds the ZIP central directory (ZIP64 aware).
2. Per file: `Range` request for exactly its bytes → C++ inflates, CRC-checks and writes to disk.
3. RAR/ISO: block headers / directory records are walked with tiny range requests; stored data is copied directly.

## Requirements
- Android 13+ (minSdk 33)
- The server must support HTTP `Range` requests (most file hosts and CDNs do)
- "All files access" permission (asked once) to create `Download/ZipStream/`

## Works well with
GitHub Releases, Internet Archive, Hugging Face, SourceForge, Pixeldrain, MediaFire, Buzzheavier,
Dropbox (`?dl=1`), most personal servers and CDNs.

## Doesn't work (yet)
Google Drive and Mega links, ad-gated/captcha hosts, expiring links mid-download, compressed RAR,
7z, UDF-only ISOs, password-protected archives.

## Disclaimer
ZipStream is a download tool. Only download content you have the right to use.

## License
MIT — see [LICENSE](LICENSE).
