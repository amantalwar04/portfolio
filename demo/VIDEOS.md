# Videos in demo/

This file embeds the MP4 and WebM videos currently in the demo/ directory and documents how to add videos and recommended best practices.

## Embedded videos

<!-- WebM first (smaller, modern) then MP4 as fallback -->
<video controls playsinline preload="metadata" poster="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/poster.jpg" style="max-width:100%;height:auto;">
  <source src="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/file_example_WEBM_1920_3_7MB.webm" type="video/webm">
  <source src="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/file_example_MP4_1920_18MG.mp4" type="video/mp4">
  Your browser does not support the video tag. You can download the MP4 directly: https://github.com/amantalwar04/portfolio/blob/main/demo/file_example_MP4_1920_18MG.mp4
</video>

- WebM file: https://github.com/amantalwar04/portfolio/blob/main/demo/file_example_WEBM_1920_3_7MB.webm
- MP4 file: https://github.com/amantalwar04/portfolio/blob/main/demo/file_example_MP4_1920_18MG.mp4

> Note: If you want the poster image to appear, add a `poster.jpg` (or png) to `demo/` or change the `poster` attribute above to point to an existing image.

---

## How to add videos

1. Place your video files under `demo/` (or create a `demo/videos/` directory if you prefer) and commit them. Example paths used here:
   - `demo/file_example_MP4_1920_18MG.mp4`
   - `demo/file_example_WEBM_1920_3_7MB.webm`
2. Add a poster/thumbnail image (e.g., `poster.jpg`) to show a preview before playback.
3. Add captions/subtitles as WebVTT files (e.g., `video.en.vtt`) and reference them with a `<track>` element:

```html
<video controls>
  <source src="/demo/your-video.webm" type="video/webm">
  <source src="/demo/your-video.mp4" type="video/mp4">
  <track kind="captions" srclang="en" label="English" src="/demo/your-video.en.vtt">
</video>
```

4. Commit and push. If the file is large (>50–100 MB) use Git LFS or host the file externally (S3, Cloudflare, Vimeo, YouTube) and embed or link to it instead.

---

## Recommended good practices

- Formats & codecs
  - Provide both WebM (VP8/VP9/AV1) and MP4 (H.264) sources so browsers can pick the best supported format.
  - MP4 (H.264 + AAC) has the widest compatibility; WebM has better compression in many cases.
- Resolution & bitrate
  - Offer multiple resolutions for responsive delivery (1080p, 720p, 480p). For demos, 720p is often sufficient.
  - Keep the bitrate appropriate for the resolution. Example: 720p -> ~1.5–4 Mbps depending on motion.
- File size & hosting
  - Keep repository-hosted video files small (a few MB) to keep the repo fast.
  - Use Git LFS for files that are consistently large or >50 MB. GitHub rejects files >100 MB.
  - For production sites, prefer CDN or object storage (S3 + CloudFront) for streaming performance.
- Accessibility
  - Provide captions (WebVTT) and a transcript for important content.
  - Add controls (use the `controls` attribute) so users can pause/seek.
  - Provide a text download link as a fallback.
- Performance
  - Use `preload="metadata"` or `preload="none"` to avoid unnecessary bandwidth usage.
  - Consider creating multiple variants and selecting the appropriate source using media queries or server-side logic.
  - Generate a poster image to avoid autoplaying long downloads.
- SEO & metadata
  - Include descriptive file names and alt-like metadata in the surrounding text.
  - Add captions and transcripts to improve discoverability and accessibility.
- Reproducible commands (ffmpeg examples)
  - Create an optimized MP4 (H.264 + AAC):

```
ffmpeg -i input.mov -vf "scale=-2:720" -c:v libx264 -preset medium -crf 23 -c:a aac -b:a 128k -movflags +faststart output-720p.mp4
```

  - Create a WebM (VP9):

```
ffmpeg -i input.mov -vf "scale=-2:720" -c:v libvpx-vp9 -b:v 0 -crf 30 -c:a libopus output-720p.webm
```

  - Generate a poster image (thumbnail):

```
ffmpeg -ss 00:00:01 -i input.mp4 -vframes 1 -q:v 2 poster.jpg
```

- File naming conventions
  - Use lowercase, hyphens, and include resolution/codec when helpful: `project-demo-720p.webm`, `project-demo-720p.mp4`.
- Security & licensing
  - Respect copyright and include licensing/attribution where required.
  - Avoid committing sensitive or private videos to a public repository.

---

If you'd like, I can:
- Add a `demo/videos/` directory and move these files there (if you want a cleaner structure).
- Generate small 480p/720p derivatives for faster demos and add captions templates.
