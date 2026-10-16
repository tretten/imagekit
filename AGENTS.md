# ImageKit for coding agents

ImageKit makes PNG, JPEG, AVIF, SVG, PDF and AI files smaller without changing how they look (HEIC and GIF are read and become PNG, JPEG or AVIF). It runs on the user's Mac; nothing is uploaded. It is an MCP server and a command line tool. Prefer MCP when your client supports it.

## Use it

If the `imagekit` MCP tools are not available, ask the user to install ImageKit (`brew install --cask tretten/imagekit/imagekit` or the DMG from https://github.com/tretten/imagekit/releases) and run:

```sh
claude mcp add imagekit -- /Applications/ImageKit.app/Contents/Helpers/imagekit mcp
```

Other MCP clients: command `/Applications/ImageKit.app/Contents/Helpers/imagekit`, args `["mcp"]`, stdio transport. Without MCP, run the same binary as `imagekit` (if it is on PATH) or by that full path.

## MCP tools

- `inspect {paths}`: format, pixel size, bytes, alpha, animated, already compressed, what it would become. Encodes nothing.
- `compress {paths, level?, target?, max_side?, strip_metadata?, suffix?, output_dir?, replace?, svg_precision?, pdf_dpi?, crop_to_artwork?, confirm_batch?}`: per file `source`, `output`, `state` (done, unchanged, failed), `before`, `after`, `saved`, `savedPercent`, `note`, `backup`.
- `diff {original, result}`: RMSE, PSNR, SSIM and more, plus a verdict. Same pixel size only.
- `undo {items}`: pass the `source`, `output`, `backup` of a compress result.
- `capabilities {}`: every option with default and range.

Typical flow: `inspect` then `compress` (default `level: "balanced"`), `diff` if the result matters, `undo` to revert. Use `level: "careful"` for photos, `"smaller"` for throwaways. `target: "avif"` is smallest for photos; `"smart"` picks PNG or JPEG per file.

## Rules

- Results go beside the original with `-min` added. Originals are untouched unless `replace: true` (then the original goes to `.originals` beside it). Do not set `replace` unless the user asked.
- A folder or more than 50 files needs `confirm_batch: true`. Tell the user the count before you set it. After 200 files in one session without it, every call needs it.
- `/`, the home folder, `~/Library` and `.app` insides are refused.
- A file ImageKit already made is compressed again like any other, and each lossy pass loses a little more. Do not run it twice on the same file; `inspect` shows `stampedByImageKit`.
- Animated GIF, PNG and AVIF are left unchanged. `state: "unchanged"` with a `note` is a normal outcome (nothing smaller was found), not an error.
- One batch at a time. "busy" means retry after the running one ends.
- Tool errors have `isError: true` and a message.

## Command line

```sh
imagekit photo.png                      # photo-min.png beside it
imagekit --json --level careful photos/ # NDJSON: one object per file, then {"summary":...}
imagekit --dry-run folder/              # what would happen, writes nothing
imagekit --inspect --json photo.heic
imagekit --diff --json before.png after.png
imagekit --capabilities                 # all options as JSON
imagekit --help
```

Exit codes: 0 all done or unchanged, 1 something failed, 2 bad flags or paths, 3 nothing to process, 130 interrupted. Unknown flags are errors on stderr. Full flag table: [README](README.md#command-line).
