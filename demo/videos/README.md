# Videos — demo/videos/

This directory contains all video assets for the portfolio, including video files, captions, transcripts, and poster images.

---

## Available videos

- `demo-video.webm` (3.7 MB) - WebM format for modern browsers
- `demo-video.mp4` (17.8 MB) - MP4 format for broad compatibility
- `demo-video.en.vtt` - English captions
- `demo-video-transcript.md` - Full text transcript
- `poster.jpg` - Thumbnail image shown before video playback

---

## Watch the video

<video controls playsinline preload="metadata" poster="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/videos/poster.jpg" style="max-width:100%;height:auto;">
  <source src="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/videos/demo-video.webm" type="video/webm">
  <source src="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/videos/demo-video.mp4" type="video/mp4">
  <track kind="captions" srclang="en" label="English" src="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/videos/demo-video.en.vtt">
  Your browser does not support the video tag. You can download the videos directly:
  - <a href="https://github.com/amantalwar04/portfolio/blob/main/demo/videos/demo-video.webm">WebM</a>
  - <a href="https://github.com/amantalwar04/portfolio/blob/main/demo/videos/demo-video.mp4">MP4</a>
</video>

---

## How to embed videos with captions

Use this HTML snippet as a template for embedding videos with captions, accessibility features, and fallback formats:

```html
<video controls playsinline preload="metadata" poster="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/videos/poster.jpg" style="max-width:100%;height:auto;">
  <source src="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/videos/demo-video.webm" type="video/webm">
  <source src="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/videos/demo-video.mp4" type="video/mp4">
  <track kind="captions" srclang="en" label="English" src="https://raw.githubusercontent.com/amantalwar04/portfolio/main/demo/videos/demo-video.en.vtt">
  Your browser does not support the video tag.
</video>
```

**Attributes explained:**
- `controls` - Shows play/pause/volume controls
- `playsinline` - Allows playback on mobile without fullscreen
- `preload="metadata"` - Loads metadata only, not the entire video
- `poster` - Shows a thumbnail before playback starts
- `<source>` - Provides multiple formats for browser compatibility
- `<track>` - Adds captions for accessibility

---

## Captions and transcripts

- **Captions (.vtt):** Help viewers who are deaf or hard of hearing, and improve comprehension in noisy environments.
- **Transcript (.md):** Provides a text version for accessibility, SEO, and searchability.

To create new captions:
1. Use a tool like Aegisub, Subtitle Edit, or even a text editor to create a `.vtt` file
2. Follow the WebVTT format: `HH:MM:SS.mmm --> HH:MM:SS.mmm` followed by caption text
3. Place the file in this directory with a language code (e.g., `video-name.en.vtt`, `video-name.es.vtt`)

---

## Best practices

✅ **Do:**
- Provide both WebM and MP4 formats for browser compatibility
- Include a poster image for better UX
- Add captions for accessibility and SEO
- Use descriptive filenames
- Keep videos compressed (<50 MB for repo hosting)

❌ **Don't:**
- Force autoplay without user interaction
- Hide controls
- Store uncompressed video files
- Forget about accessibility

---

## Adding new videos

1. Convert/compress your video to WebM and MP4 formats
2. Generate a poster image: `ffmpeg -ss 00:00:01 -i video.mp4 -vframes 1 poster.jpg`
3. Create captions in WebVTT format
4. Add transcript in Markdown
5. Update this README with the new video

See the main `demo/video.md` for detailed ffmpeg commands.
