# Videos — demo/video.md

This file documents the videos available in the repo (MP4 and WebM), shows how to embed them, and provides detailed instructions and recommended best practices for adding and managing videos in this repository.

---

## Available videos (in repo/demo/)

- demo/file_example_WEBM_1920_3_7MB.webm
  - URL: https://github.com/amantalwar04/portfolio/blob/main/demo/file_example_WEBM_1920_3_7MB.webm
- demo/file_example_MP4_1920_18MG.mp4
  - URL: https://github.com/amantalwar04/portfolio/blob/main/demo/file_example_MP4_1920_18MG.mp4

---

## Embedded example (WebM first, MP4 fallback)

Use this HTML snippet in markdown or an HTML page to embed the videos. The poster attribute is optional — add `demo/poster.jpg` (or point to an existing image) if you want a thumbnail shown before playback.

```html
<video controls playsinline preload="metadata" poster="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/poster.jpg" style="max-width:100%;height:auto;">
  <source src="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/file_example_WEBM_1920_3_7MB.webm" type="video/webm">
  <source src="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/file_example_MP4_1920_18MG.mp4" type="video/mp4">
  Your browser does not support the video tag. You can download the MP4 directly: https://github.com/amantalwar04/portfolio/blob/main/demo/file_example_MP4_1920_18MG.mp4
</video>
```

To add captions/subtitles, include a <track> element (WebVTT files):

```html
<video controls>
  <source src="/demo/your-video.webm" type="video/webm">
  <source src="/demo/your-video.mp4" type="video/mp4">
  <track kind="captions" srclang="en" label="English" src="/demo/your-video.en.vtt">
</video>
```

---

## How to add videos to this repository

1. Choose where to place videos
   - For small demo files (a few MB), keeping them in `demo/` is fine.
   - For a clearer structure, create `demo/videos/` and add all video assets there.
2. File size considerations
   - Keep repository-hosted videos small (<50 MB) when possible.
   - Files >50 MB should use Git LFS; files >100 MB are rejected by GitHub.
   - For production or large assets, use external hosting (S3/CloudFront, Cloudflare R2, Vimeo, YouTube) and embed or link to the external URL.
3. Add a poster/thumbnail image
   - Create a thumbnail `poster.jpg` with ffmpeg or an image editor and add it to the same directory.
4. Provide captions and transcripts
   - Create WebVTT files (e.g., `video.en.vtt`) for captions.
   - Provide a plain-text transcript for accessibility and SEO.
5. Commit and push
   - If you must add large files, enable Git LFS: `git lfs install && git lfs track "*.mp4" "*.webm"` then `git add .gitattributes`.

---

## Recommended good practices (detailed)

- Formats & codecs
  - Offer both WebM (VP8/VP9/AV1) and MP4 (H.264 + AAC) so browsers choose the best supported format.
  - MP4 (H.264) provides the broadest compatibility; WebM often produces smaller files for the same quality.
- Resolution & bitrate
  - Provide multiple resolutions (1080p, 720p, 480p) for responsive delivery.
  - Example bitrates: 720p => ~1.5–4 Mbps depending on motion.
- File size & hosting
  - Keep repo-hosted assets small. For larger or many videos, use Git LFS or external hosting/CDNs.
  - Prefer hosting on a CDN or object storage behind a CDN for production to reduce latency.
- Accessibility
  - Always include captions (WebVTT) and an accessible transcript.
  - Ensure controls are available (use `controls`) and avoid forcing autoplay.
  - Provide a text download link for users who cannot play embedded video.
- Performance
  - Use `preload="metadata"` or `preload="none"` to prevent unnecessary data fetching.
  - Use a poster image so the page doesn't start loading large video blobs immediately.
  - If you need adaptive streaming, consider HLS/DASH served from a CDN rather than multiple static files.
- SEO & metadata
  - Use descriptive filenames and surrounding copy to improve discoverability.
  - Include captions and transcripts.
- Naming conventions
  - Use lowercase, hyphens, and include resolution or quality when helpful: `project-demo-720p.webm`.
- Legal & security
  - Respect copyright. Don't commit private or proprietary videos to a public repo.

---

## Helpful ffmpeg commands

Optimize and create target variants with ffmpeg. Replace `input.mov` with your source.

Create an MP4 (H.264 + AAC) at 720p:

```bash
ffmpeg -i input.mov -vf "scale=-2:720" -c:v libx264 -preset medium -crf 23 -c:a aac -b:a 128k -movflags +faststart output-720p.mp4
```

Create a WebM (VP9):

```bash
ffmpeg -i input.mov -vf "scale=-2:720" -c:v libvpx-vp9 -b:v 0 -crf 30 -c:a libopus output-720p.webm
```

Generate a poster image at 1 second:

```bash
ffmpeg -ss 00:00:01 -i input.mp4 -vframes 1 -q:v 2 poster.jpg
```

Generate a low-resolution copy (480p) for fast demos:

```bash
ffmpeg -i input.mp4 -vf "scale=-2:480" -c:v libx264 -preset fast -crf 28 -c:a aac -b:a 96k output-480p.mp4
```

---

## Suggested next actions I can take for you

- Create `demo/videos/` and update this file to reference the new paths.
- Move the existing video files into `demo/videos/` (note: moving large binary files within git will rewrite history only if you rebase — otherwise it's a normal move in a new commit). I can add a commit that adds copies in `demo/videos/` and then remove the originals if you prefer.
- Add `demo/poster.jpg` (I can create a poster by extracting a frame if you want).
- Create WebVTT caption templates for the videos.

Tell me which of the above you'd like me to do next and I'll proceed.
