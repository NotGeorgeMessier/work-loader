# Work loader (video)

The loader is **a short looping video** (`loader.mp4`). Everything around it—size, shape, ring, backdrop, when it plays—is **styling and app logic** you control.

**Full reference implementation:** see [`index.html`](./index.html) for layout, CSS (circular clip, optional spinning ring), and play / pause / tap-to-toggle behavior.

---

## Minimal HTML

Replace `src` with your own URL or path if you self-host the file.

```html
<video
  src="https://raw.githubusercontent.com/NotGeorgeMessier/work-loader/main/loader.mp4"
  playsinline
  preload="auto"
></video>
```

To start playback from script (after a user gesture if the browser requires it), handle the promise from `play()`:

```html
<script>
  const video = document.querySelector("video");
  function playLoader() {
    if (video.ended) video.currentTime = 0;
    video.play().catch(() => {});
  }
</script>
```

---

## Minimal React

```tsx
import { useRef } from "react";

export function LoaderVideo() {
  const ref = useRef<HTMLVideoElement>(null);

  function play() {
    const el = ref.current;
    if (!el) return;
    if (el.ended) el.currentTime = 0;
    el.play().catch(() => {});
  }

  return (
    <video
      ref={ref}
      src="https://raw.githubusercontent.com/NotGeorgeMessier/work-loader/main/loader.mp4"
      playsInline
      preload="auto"
    />
  );
}
```

Use `play()` from a click handler or after your app is ready; avoid assuming autoplay will succeed without `muted` (see below).

---

## License

MIT — see [LICENSE](./LICENSE).
