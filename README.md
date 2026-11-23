<p align="center">
  <img src="https://i.postimg.cc/tCQ0vvRR/banner.png" alt="ClipShrink Video Compressor — Compress Gameplay Clips to Exact 10 MB / 50 MB Limits" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-Video%20Compressor-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-clipshrink--v1.4-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# ClipShrink Video Compressor — Compress Gameplay Clips to Exact 10 MB / 50 MB Limits

**Discord rejecting your 120 MB ShadowPlay or OBS clip with 'Your files are too powerful'? Tired of blurry online compressors with upload queues and watermarks? Drag and drop any video to hit 10 MB, 25 MB, or 50 MB locally in seconds.**

ClipShrink Video Compressor wraps precision two-pass bitrate calculation and hardware-accelerated encoding into a simple portable Windows window: **automatically measuring clip duration and audio bitrate so the output MP4 lands cleanly under Discord's 10 MB free tier or custom MB targets**.

This project is aimed at **Windows 10 and Windows 11 (64-bit) PC users** sharing gameplay highlights, bug reports, and screen recordings on Discord, Telegram, Slack, and Reddit—100% offline with zero file uploads.

## Quick Use-Case & Troubleshooting Reference

| Scenario / Issue | Cause | Solution |
| --- | --- | --- |
| Discord blocks clip ('Your files are too powerful' > 10 MB) | Raw ShadowPlay / OBS clips recorded at 30–50 Mbps exceed free upload cap | Select the `10 MB (Discord)` preset for exact two-pass target sizing |
| Online video compressors take minutes to upload 500 MB files | Cloud tools require uploading the full source clip before compressing | Encode locally on your own GPU in seconds with zero internet upload |
| Single-pass compression overshoots target MB size | Constant CRF encoding cannot guarantee a strict file-size ceiling | Use automatic two-pass bitrate math (`TargetBits / Duration - AudioBits`) |
| Long 3-minute clips look pixelated at 10 MB | 1080p60 resolution starved for bitrate over long durations | Enable automatic 720p30 smart downscale when bitrate drops below threshold |

## Download for Windows

[**Download ClipShrink.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/ClipShrink.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why use `ClipShrink.exe`? (Key features)

- Calculates exact video + audio bitrates from clip duration so output files never exceed `9.8 MB` / `24.5 MB` / `49.5 MB`.
- Supports drag-and-drop batch processing for `.mp4`, `.mkv`, `.mov`, `.avi`, and `.webm` recordings.
- Uses NVIDIA NVENC, AMD VCE/AMF, or Intel QSV hardware acceleration when available.
- Preserves original source files untouched and writes `*_10MB.mp4` next to the input video.

### Sample Output

```text
[ClipShrink] Loaded: EldenRing_BossFight.mkv (00:42 | 1920x1080 60fps | 164.2 MB)
[INFO] Target Preset    : Discord Free (Max 10.0 MB -> Target 9.6 MB)
[INFO] Bitrate Math     : Video 1,760 kbps + AAC Audio 96 kbps (Smart 720p60)
[OK]   Encoded Output   : EldenRing_BossFight_10MB.mp4 (9.48 MB in 3.1s)
```

The release ZIP is named `ClipShrink.zip`; the Windows executable inside is named `ClipShrink.exe`.

1. Close ClipShrink before updating or replacing executable files.
2. Click **Download ClipShrink.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `ClipShrink.exe`.
5. Review the options and output paths before processing files.

**Requirements:** Windows 10 or 11 (64-bit); supports NVIDIA NVENC, AMD AMF, Intel QuickSync, and CPU fallback.

### Verification & Windows SmartScreen Note

- **Offline & standard user permissions:** `ClipShrink.exe` runs locally without uploading your files and does not require disabling Windows Defender.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project solves

### Exact file-size targeting without trial-and-error

Guessing CRF values wastes time when you need a clip to fit strictly inside Discord's 10 MB, Nitro Basic's 50 MB, or email's 25 MB limit.

### No command-line syntax or FFmpeg scripts to memorize

Instead of typing complex two-pass terminal commands, drop one or twenty clips into the window and pick a size preset.

### Smart resolution & FPS scaling for longer clips

Automatically stepping down from 1080p60 to 720p30 on longer clips keeps text and HUD elements sharp instead of blocky.

### 100% private local processing

Your screen recordings and private chats never leave your PC.

## Default folders and configuration paths

ClipShrink runs as a portable Windows folder and outputs compressed files alongside your source videos:

```text
%USERPROFILE%\Videos\Captures\
```

Typical directory layout:

```text
Videos\Captures\
├── GameplayClip.mp4          (Original 148.0 MB)
└── GameplayClip_10MB.mp4     (Compressed 9.52 MB — Ready for Discord)
```

Original source videos are never overwritten or deleted during compression.

## Quick start guide

Follow these steps to get started:

1. **Extract `ClipShrink.zip` to a local folder.** Avoid running directly from inside Windows Explorer's temporary ZIP preview.
2. **Launch `ClipShrink.exe` and drag your `.mp4` or `.mkv` clips onto the window.** You can drop individual files or an entire folder.
3. **Choose a size preset (`10 MB Discord`, `25 MB Email`, `50 MB Telegram`, or custom MB).** Optionally toggle 720p downscaling for clips longer than 45 seconds.
4. **Click **Compress** and wait a few seconds.** Hardware acceleration encodes typical 30-second clips in 2–4 seconds.
5. **Drag the resulting `*_10MB.mp4` file directly into Discord or Telegram.** Verify playback and audio sync before sharing.

### Data safety note

Source files remain untouched; output files are saved with a size suffix in the same directory unless a custom output folder is chosen.

## What the status summary shows

ClipShrink displays **source duration, resolution, calculated target bitrate, hardware encoder status, and final output MB size** for every processed clip.

## FAQ

**Does ClipShrink upload my videos to a server?**

No. All compression happens 100% locally on your Windows PC.

**Why is the output file ~9.5 MB when I pick the 10 MB preset?**

Leaving a ~0.4 MB safety margin guarantees Discord and Telegram never reject the file due to MP4 container overhead.

**What video formats are supported?**

MP4, MKV, MOV, AVI, WebM, FLV, and WMV.

## Useful reading

- [FFmpeg Official Documentation](https://ffmpeg.org/documentation.html)

## More Windows Desktop Utilities

- [SnapFormat-BatchMediaConverter](../SnapFormat-BatchMediaConverter) — Offline batch HEIC/WebP/MKV to JPG/PNG/MP4 converter
- [WhisperDesk-OfflineTranscriber](../WhisperDesk-OfflineTranscriber) — Local offline speech-to-text & SRT subtitle generator
- [CleanCut-OfflineBgRemover](../CleanCut-OfflineBgRemover) — Offline batch image background remover & PNG cutout tool
- [ExifScrub-PhotoMetadataCleaner](../ExifScrub-PhotoMetadataCleaner) — Strip GPS, EXIF & camera metadata from photos offline

*Independent open-source desktop utility for Windows. Not affiliated with Discord Inc. or Telegram.*
