# Work loader (video)

The loader is **a short looping video** (`loader.mp4`). Everything around it — size, shape, ring, backdrop, when it plays — is **styling and app logic** you control.

**Full reference implementation:** see `[index.html](./index.html)` for layout, CSS (circular clip, optional spinning ring), and play / pause / tap-to-toggle behavior.

---

## Plain

<video src="https://raw.githubusercontent.com/NotGeorgeMessier/work-loader/main/web-loader-example.mp4" controls playsinline width="400"></video>

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

## React

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

## React Native

<video src="https://raw.githubusercontent.com/NotGeorgeMessier/work-loader/main/react-native-loader-example.mp4" controls playsinline width="400"></video>

```tsx
import { Pressable, View } from 'react-native';
import { useVideoPlayer, VideoView } from 'react-native-video';

export const VideoSampleCode = () => {
  const player = useVideoPlayer(
    'https://raw.githubusercontent.com/NotGeorgeMessier/work-loader/main/loader.mp4',
    _player => {
      _player.preload();
    },
  );

  return (
    <View style={{ alignItems: 'center', justifyContent: 'center' }}>
      <Pressable
        onPress={() => {
          player.seekTo(0);
          player.play();
        }}
      >
        <VideoView
          player={player}
          resizeMode="cover"
          style={{
            width: 60,
            aspectRatio: 1,
            borderRadius: 1000,
            overflow: 'hidden',
          }}
        />
      </Pressable>
    </View>
  );
};
```

---

## License

MIT — see [LICENSE](./LICENSE).