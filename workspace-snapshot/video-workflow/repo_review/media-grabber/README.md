<div align="center">

<img src="assets/logo.svg" alt="Media Grabber" width="560" />

### A free, open-source video and audio downloader for Chrome — find and save media from any web page

<a href="https://chromewebstore.google.com/detail/ddabljeecabankgggocbidpkhgiggjeo">
  <img src="https://img.shields.io/badge/Chrome%20Web%20Store-Install%20Now-4f46e5?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Install from the Chrome Web Store" />
</a>

<br /><br />

[![Chrome Web Store Version](https://img.shields.io/chrome-web-store/v/ddabljeecabankgggocbidpkhgiggjeo?label=version)](https://chromewebstore.google.com/detail/ddabljeecabankgggocbidpkhgiggjeo)
[![Chrome Web Store Users](https://img.shields.io/chrome-web-store/users/ddabljeecabankgggocbidpkhgiggjeo?label=users)](https://chromewebstore.google.com/detail/ddabljeecabankgggocbidpkhgiggjeo)
[![Chrome Web Store Rating](https://img.shields.io/chrome-web-store/rating/ddabljeecabankgggocbidpkhgiggjeo?label=rating)](https://chromewebstore.google.com/detail/ddabljeecabankgggocbidpkhgiggjeo)
[![License: MIT](https://img.shields.io/badge/License-MIT-4f46e5.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-22c55e.svg)](CONTRIBUTING.md)
[![Stars](https://img.shields.io/github/stars/riponcm/media-grabber?style=social)](https://github.com/riponcm/media-grabber/stargazers)

</div>

---

**Media Grabber is a free, open-source video downloader, audio downloader and tab recorder
extension for Chrome.** It detects the real media source behind any web page so you can save
audio and video in one click — even when the site offers no download button.

Built as a dependency-free Manifest V3 extension, it also reads adaptive **HLS and DASH**
streams (`.m3u8`, `.mpd`) to list every available quality, saves HLS streams directly by
joining their segments, and includes a **browser audio recorder** for media that is streamed
in memory and cannot be saved as a file.

_An open-source project by **[Matily](https://matily.org)** — free, non-profit software for everyone._

> If this project saves you time, please consider giving it a star. It takes one click, costs you
> nothing, and is the single best way to help other people discover it.

## Demo

A quick run through detection, one-click download, and the built-in recorder:

<div align="center">
  <img src="assets/demo.gif" alt="Media Grabber in action — detect, download, and record" width="720" />
</div>

## Screenshots

<div align="center">

**Find and download media from any page** — the toolbar popup lists every audio and video
source it finds, with format, size and a one-click download.

<img src="assets/screenshot-detect.png" alt="Video downloader popup listing detected MP4 and HLS media with quality and file size" width="820" />

<br />

**Every quality, ranked best first** — Media Grabber reads the stream manifest and lists each
rendition, so you are never stuck with the low-bitrate copy the player happened to load.

<img src="assets/screenshot-quality.png" alt="Media Grabber listing 1080p and 720p renditions of the same video" width="820" />

<br />

**Record tab audio, microphone, or both** — a docked side panel with a live waveform,
pause and resume, and WebM or WAV output.

<img src="assets/screenshot-recorder.png" alt="Browser audio recorder extension capturing tab audio with a live waveform" width="820" />

<br />

**Save streams without extra tools** — HLS segments are fetched and joined into a single
file, with no re-encoding and no quality loss.

<img src="assets/screenshot-streams.png" alt="HLS stream downloader progress showing segments being joined into one file" width="820" />

</div>

## Features

- **Network detection.** Watches response content types and catches media files
  (`mp3`, `m4a`, `aac`, `ogg`, `wav`, `flac`, `mp4`, `webm`, `mov`, and more).
- **Page detection.** Scans the DOM for `<audio>` and `<video>` elements, including the source
  that is actually playing.
- **One-click downloads.** Saves direct files through the browser's own download manager.
- **Quality selection.** Reads the stream manifest and lists every rendition it offers
  (1080p, 720p, and so on), ranked highest first, so you never end up with the low-bitrate
  copy an adaptive player happened to load.
- **Stream support.** Detects HLS and DASH playlists (`.m3u8`, `.mpd`). HLS streams can be
  saved directly — segments are fetched and joined into one file with no re-encoding — and a
  copy-paste FFmpeg command is offered for everything else.
- **Right-click downloads.** A context-menu entry lists the media found on the page so you can
  save it without opening the popup.
- **Audio recorder.** A docked **side panel** captures **tab audio, microphone, or both
  mixed** — ideal for streams that can't be saved directly (in-memory MediaSource / blob).
  Live **waveform**, **pause/resume**, preview before saving, and **WebM** (Opus) or **WAV**
  (lossless) output — both native, no dependencies.
- **Per-tab badge.** Shows how many media items were found on the current tab.
- **Private by design.** No accounts, no tracking, no external servers. Everything runs locally.

## Capabilities and limits

| Media type | Detect | Download |
| --- | :---: | :---: |
| Direct files (`mp3`, `mp4`, `webm`, ...) | Yes | Yes, one click |
| HTML5 `<audio>` / `<video>` with a URL | Yes | Yes |
| HLS streams (`m3u8`) | Yes | Yes — segments joined into one file |
| DASH streams (`mpd`) | Yes | Via the generated FFmpeg command |
| In-page MediaSource / blob streams | Yes | Use the built-in **recorder** |
| DRM-protected media | No | No — encrypted, and not bypassed |
| YouTube | No | Not supported, per Chrome Web Store policy |

## Installation

### From the Chrome Web Store (recommended)

**[➜ Install Media Grabber](https://chromewebstore.google.com/detail/ddabljeecabankgggocbidpkhgiggjeo)** — one click, with automatic updates.

### From source (for developers)

No build step required:

1. Download or clone this repository.
2. Open Chrome and go to `chrome://extensions`.
3. Enable **Developer mode** using the toggle in the top-right corner.
4. Click **Load unpacked** and select the project folder.
5. Pin **Media Grabber** from the extensions menu.

## Usage

1. Open a page and start playing the audio or video.
2. Click the Media Grabber toolbar icon to see detected media.
3. Press **Download** for files, or **Copy FFmpeg** for streams and run the command:
   ```bash
   ffmpeg -i "STREAM_URL" -c copy "output.mp4"
   ```
4. Use the re-scan button if media loads late.

## Frequently asked questions

### How do I download a video from a website that has no download button?

Open the page, start the video, then click the Media Grabber icon. The extension watches what
the page loads, so any playable audio or video appears in the list with a **Download** button.
If the media loads late, press re-scan.

### Why does my downloaded video have no sound?

Because many sites use adaptive streaming, which delivers picture and sound as **two separate
files**. Downloading only the video track gives you a silent file. Download both entries, then
use the **Merge video + audio** button, which copies this command to your clipboard:

```bash
ffmpeg -i "video.mp4" -i "audio.m4a" -c copy "output.mp4"
```

`-c copy` merges without re-encoding, so it is instant and lossless.

### Why is my downloaded video low quality?

Adaptive streams start at a low bitrate and increase as the connection allows, so a naive
download captures whatever rendition the player fetched first. Media Grabber reads the stream
manifest and lists every available quality, ranked highest first — pick the top entry.

### Several files are listed. Which one should I download?

The list is sorted best-first, and each row shows its format (MP4, WEBM, M4A, HLS, DASH) and
file size. The top entry is normally the one you want; a much smaller entry alongside it is
usually the separate audio track.

### What are HLS and DASH, and how do I save them?

They are adaptive streaming formats that split a video into many small segments described by a
playlist (`.m3u8` for HLS, `.mpd` for DASH). Media Grabber can save HLS directly: press
**Save** and it downloads every segment and joins them into a single file with no re-encoding.
DASH streams come with a ready-to-run FFmpeg command instead.

### Can I record audio that is playing in a browser tab?

Yes. Open the recorder side panel and choose **tab audio**, **microphone**, or **both mixed**.
You get a live waveform, pause and resume, and a preview before saving as WebM (Opus) or WAV
(lossless). The audio keeps playing normally while it is captured, so recording is the reliable
option for media that is streamed in memory and cannot be saved as a file.

### Does Media Grabber work on YouTube?

No. Chrome Web Store policy does not permit extensions that download YouTube content, so
YouTube is deliberately excluded and the extension does not operate on it.

### Can it download Netflix, Spotify, or other DRM-protected media?

No. That content is encrypted with DRM, which Media Grabber does not attempt to bypass. This is
both a technical and a deliberate design limit.

### Does the extension collect any of my data?

No. There are no accounts, no analytics, and no external servers. Detection, downloading and
recording all happen locally in your browser, and the source code is public in this repository.

### Is Media Grabber free?

Yes — free and open source under the MIT licence, with no paid tier, no ads and no upsells.
It is built by [Matily](https://matily.org), a non-profit software studio.

### Do I need FFmpeg installed?

Not for most tasks. Direct files and HLS streams are saved by the extension itself. FFmpeg is
only needed to merge separate video and audio tracks, or to save a DASH stream — and the exact
command is generated and copied for you.

## How it works

```
                 +------------------------+
  network ─────► |   background worker    |
  responses      |  (webRequest sniffer)  | ──┐
                 +------------------------+   │   per-tab,
                                              ├─► de-duplicated  ──► popup UI
                 +------------------------+   │   media list
  page DOM ────► |     content script     | ──┘
  <audio>/<video>|  (element scanner)     |
                 +------------------------+
```

- `src/background.js` observes `webRequest` responses and classifies them by content type.
- `src/content.js` scans the page for media elements and reports them.
- `src/popup.js` renders the combined list and triggers downloads.

## Project structure

```
media-grabber/
├─ manifest.json          Extension manifest (Manifest V3)
├─ src/
│  ├─ background.js        Network sniffer and per-tab media store
│  ├─ content.js           DOM media scanner
│  ├─ popup.html           Toolbar UI
│  ├─ popup.css            Toolbar styles
│  ├─ popup.js             Toolbar logic
│  ├─ recorder.html        Recorder window UI
│  ├─ recorder.css         Recorder window styles
│  └─ recorder.js          Tab/mic capture, mixing, WebM/WAV encoding
├─ icons/                  Toolbar icons (16, 32, 48, 128)
└─ assets/                 Logo and brand assets
```

## Responsible use

Use Media Grabber only for media you have the right to download, such as your own files,
public-domain or Creative Commons content, or media you are licensed to keep. Respect the terms
of service of the sites you visit and all applicable copyright law. The extension deliberately
does not attempt to bypass DRM.

## Changelog

Release notes for every version live in [CHANGELOG.md](CHANGELOG.md).

## Contributing

Contributions are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) and open an issue or
pull request. If you like the direction of the project, a star is a great way to show support.

## Topics

chrome-extension · video-downloader · audio-downloader · media-downloader · video-download-helper ·
audio-recorder · tab-audio-recorder · screen-audio-recorder · recorder-extension ·
hls-downloader · m3u8-downloader · dash · mpd · stream-downloader · ffmpeg ·
manifest-v3 · browser-extension · javascript · privacy-first · open-source

## License

Released under the [MIT License](LICENSE). © Matily.

<div align="center">

If Media Grabber is useful to you, consider starring the repository.

[![Star this repo](https://img.shields.io/github/stars/riponcm/media-grabber?style=for-the-badge&logo=github&color=4f46e5)](https://github.com/riponcm/media-grabber)

</div>
