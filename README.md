<h1 align="center">ImageKit</h1>

<p align="center">
  <img src="logo.png" width="128" alt="ImageKit icon">
</p>

<p align="center">
A Mac app that makes PNG, JPEG, AVIF, SVG, and PDF files smaller without changing how they look, and turns Illustrator logos into PDF or SVG. Drop files or folders on it, or right-click a file in Finder, and compare the result with the original before you keep it. Everything runs on your Mac; nothing is uploaded.
</p>

<p align="center">
  <a href="https://github.com/tretten/imagekit/releases/latest/download/ImageKit.dmg">
    <img src="download-macos.svg" width="260" alt="Download for macOS">
  </a>
</p>

## Features

- Two modes, switched at the top left (⌘1 and ⌘2): Raster for PNG, JPEG, and AVIF, Vector for SVG, PDF, and Illustrator (AI) files. Dropping files of the other kind switches the mode for you.
- Compresses PNG, JPEG, and AVIF. PNGs are reduced to a palette with the fewest colors that still match the original, then packed with Zopfli. JPEGs are re-encoded with mozjpeg at the lowest quality that keeps the picture alike, and never end up larger than a lossless rewrite of the same file. AVIF uses the system encoder.
- Vector: SVG files lose metadata, editor data, comments, and empty groups, and get shorter numbers and paths, checked against a render of the original. PDF files get their images recompressed at the JPEG quality and resolution you pick, with text, links, and bookmarks kept.
- Illustrator (AI) files convert to PDF (artboard and transparency kept, private Illustrator data dropped) or to SVG for the web, with an option to crop the empty margin around the artwork. The SVG conversion covers paths, strokes, gradients, clipping, and CMYK and spot colors, and a note on the row says what it could not carry over, such as live text. Outline the text in Illustrator first.
- Three quality levels: Smaller, Balanced, and Closest.
- Keeps each file's format, picks the smaller of PNG and JPEG per file, or converts everything to PNG, JPEG, or AVIF.
- Limits the longest side of large images (1024, 2048, 2560, or 4096 px), sets a 72 or 96 dpi tag, and removes camera and location data from JPEGs. A photo saved sideways is rotated upright first.
- Safe by default: the result is saved beside the original with a suffix you choose (`-min`). Or it replaces the file and the original goes to the Trash or to an `.originals` folder. Undo puts the last batch back.
- Before and after preview with a draggable slider, a Fit view, and a 100% view you can pan, so you can judge the quality at real pixels. Arrow keys step through the batch.
- Folders and batches: a dropped folder or more than ten files waits in a list until you press Compress. Files run in parallel on all cores, each row fills as it progresses, and Stop cancels the rest.
- Ways in: drag onto the window or the Dock icon, Choose…, the Finder right-click menu (Quick Actions › Compress with ImageKit), a global shortcut that compresses what is selected in Finder (⌘⇧K by default, configurable), and the menu bar icon.
- Works in the background: files dropped on the menu bar icon, sent by the shortcut or by the Quick Action are compressed with your settings without opening the window, and a notification says what was saved.
- Shows in the Dock, the menu bar, or both.
- Marks the files it makes, so a compressed file is not squeezed a second time and does not lose more quality.
- Checks for updates with Sparkle, daily and on every launch.

## Privacy

Runs entirely on your Mac. No analytics, no uploads. The only network connection is Sparkle's update check (daily and on every launch). The shortcut asks macOS once for permission to read Finder's selection. The right-click menu needs no permission.

## Install

Download the latest DMG from [Releases](https://github.com/tretten/imagekit/releases), drag ImageKit to Applications, and open it. Builds are signed and notarized. Requires macOS 14 (Sonoma) or later on a Mac with Apple silicon.

To get the right-click menu, open System Settings › Extensions › Finder (or Quick Actions) and turn on **Compress with ImageKit**.

## Third-party software

ImageKit includes [Zopfli](https://github.com/google/zopfli) (Apache 2.0), [mozjpeg](https://github.com/mozilla/mozjpeg) (IJG, BSD, and zlib licenses), and [Sparkle](https://sparkle-project.org) (MIT). The full notices are in the app under Settings › About.

---

This repository holds only signed release builds (DMG/ZIP) for the auto-update feed. It does not contain source code.
