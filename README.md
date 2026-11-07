# Media Player (Android)

Video + music player. Kotlin, Jetpack Compose, Media3 ExoPlayer. Min Android 8.0 (API 26).

## Build
1. Open this folder in **Android Studio** (Koala or newer) and let Gradle sync.
2. Run on a phone or emulator. Allow media access when asked.
3. APK: *Build > Build Bundle(s) / APK(s) > Build APK(s)*.

## Features
| You asked for | How it works |
|---|---|
| Clean main screen with folders | Library lists every folder that contains video or music, with counts. Filter: All / Videos / Music. |
| Red **NEW** tag | Files added after the app was first opened are tagged NEW, and so are their folders (folders with new items sort first). The tag clears when you play the file. Rescanned each time the app opens. |
| Screen size adjustment | Top bar button cycles Fit, Stretch, Crop, Fit width, Fit height. Rotate button forces landscape. |
| Brightness | Swipe up/down on the **left** half of the video. |
| Sound | Swipe up/down on the **right** half; music screen has a volume slider. |
| Fast forward | Double-tap right/left = +/-10 s, swipe sideways to scrub, 10 s buttons, seek bar, speed button (0.5x to 2x). |
| Resume | Position saved every 3 s and on pause/skip/close, per file. Reopening the file continues from there (shown as "Resume at ..." in the folder list). Cleared when a file finishes. |
| Background play | Playback runs in a foreground media service with notification and lock-screen controls. Keeps playing when the app is closed or the screen is off. |
| Equalizer | Equalizer button (video and music): on/off, presets, per-band sliders. Settings are remembered. |
| All formats | Uses Android's built-in decoders through ExoPlayer: MP4, MKV, WebM, 3GP, TS, FLV, MP3, AAC, FLAC, OGG, OPUS, WAV, M4A, AMR, MIDI and more. Anything the phone's hardware can't decode (some HEVC/AC3/DTS files) needs the optional FFmpeg extension (see below). |

## Notes
- Written without access to the Android SDK, so it has **not been compiled or run**. If Gradle reports a version or import error, send it to me and I'll fix it.
- No launcher icon is included (Android uses a default). Add one via *New > Image Asset* in Android Studio.
- For even wider codec coverage (AC3, DTS, ALAC, etc.), build Media3's FFmpeg decoder extension and add it as a dependency; the player is already set to use extension renderers when present.
- Code map: `PlayerHub` (player, resume, equalizer) · `PlaybackService` (background) · `MediaScanner` (folders, NEW) · `HomeScreen`/`FolderScreen` · `VideoPlayerScreen`/`AudioPlayerScreen` · `EqualizerDialog`.
