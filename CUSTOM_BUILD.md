# Custom LibAV Build for Easy YouTube Video Downloader

This fork of libav.js includes custom JavaScript glue code for enhanced HTTP fetching capabilities.

## Customizations

The following custom modifications are included via `custom-post.js`:

1. **FetchWithRetry**: Robust fetch with exponential backoff (3 retries, 1s initial backoff).
2. **abortSignalAny**: Polyfill for `AbortSignal.any()` for browsers without native support.
3. **Enhanced jsfetch protocol**: Integrates retry logic and external abort controller support.

## Building (Verification for Mozilla AMO)

### Option 1: GitHub Actions (Recommended)

1. Fork or clone this repository to your GitHub account.
2. Go to **Actions** → **Manual Build h264-aac-mp3**.
3. Click **Run workflow**.
4. Once complete, download the **libav-h264-aac-mp3** artifact from the workflow run.

The output files in `dist/` should match the distributed binaries.

### Option 2: Local Build

Prerequisites: Docker or Emscripten SDK (v3.1.71), Node.js 20+

```bash
# Clone the repository
git clone <repo-url>
cd libav-patched-6571

# Extract sources
make extract

# Build the h264-aac-mp3 variant
make build-h264-aac-mp3 -j$(nproc)
```

Output will be in `dist/`.

## Files Modified

| File | Change |
|------|--------|
| `Makefile` | Added `--post-js custom-post.js` to `EFLAGS` |
| `custom-post.js` | Custom JavaScript (FetchWithRetry, abort handling) |

## For Mozilla AMO Reviewers

1. Clone this repository.
2. Run the GitHub Actions workflow **Manual Build h264-aac-mp3**.
3. Compare the output `libav-6.5.7.1-h264-aac-mp3.wasm.mjs` with the distributed file.

This setup clearly separates upstream libav.js from the custom glue code (`custom-post.js`), making verification straightforward.
