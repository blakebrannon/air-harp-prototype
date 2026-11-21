# Air Harp

A self-contained browser prototype of an air harp, built for testing inside [AskWolfie](https://askwolfie.whitefieldacademy.com). Pinch with both hands in front of a webcam to draw glowing strings of light, then sweep a fingertip across a string to pluck it. String length sets the pitch and is snapped to a pentatonic scale so every string sounds musical. Mouse and touch work as a fallback when no camera is available.

There is no build step. Open `index.html` over HTTPS (or `localhost`) in a current desktop Chrome or in iPhone Safari.

## Live demo

Once GitHub Pages is on, the prototype will be at:

https://blakebrannon.github.io/air-harp-prototype/

The files are already on the `main` branch. Pages still has to be turned on once in the repository settings (the GitHub API token used here cannot create a Pages site):

1. Open https://github.com/blakebrannon/air-harp-prototype/settings/pages
2. Under **Build and deployment**, set Source to **GitHub Actions**, or to **Deploy from a branch** with branch `main` and folder `/ (root)`.
3. Wait a minute, then open the URL above. After that, phone testing and AskWolfie embedding will work over HTTPS.

## How to use

1. Tap **Start camera** and allow the camera prompt. Sound unlocks on that first tap.
2. Pinch thumb and index on both hands, pull your hands apart to draw a string, then release to set it. Longer strings play lower notes; shorter strings play higher ones.
3. Sweep an index fingertip across a string to pluck it. The string vibrates and a spark runs along it.
4. Or click/tap and drag to draw, then move across a string to pluck, if you are testing without a camera.
5. Use **Test sound**, **Undo**, and **Clear** as needed. Up to 12 strings can be on screen at once.

## Embed in AskWolfie

The page must be served over HTTPS. Camera access requires a secure context, and a cross-origin iframe needs an explicit permission policy:

```html
<iframe
  src="https://blakebrannon.github.io/air-harp-prototype/"
  allow="camera; autoplay"
  style="width:100%; height:100%; border:0;"
  title="Air Harp"
></iframe>
```

## Local preview

```bash
python3 -m http.server 8765 --directory .
# then open http://localhost:8765/
```

## Technical notes

- Hand tracking uses Google MediaPipe Tasks Vision (`@mediapipe/tasks-vision` from jsDelivr, Apache-2.0) with the GPU delegate in VIDEO mode and a CPU fallback. Detection is capped at about 30 fps.
- The plucked tone is an original Karplus–Strong implementation written for this file. It does not use code from PlayTheNote, Fili di luce, Jalalkhan, or other third-party harp demos.
- Audio starts on the first user gesture so iPhone Safari will play sound.
- The video element is `playsinline` and muted, and the canvas resizes on orientation changes.

## Known limitations

- iPhone Safari requires a tap on **Start camera** before the webcam can open, and the page must be served over HTTPS.
- When this page is iframed, the host must set `allow="camera; autoplay"`.
- The first hand-tracking model download can take a few seconds on a slow connection.
- Some devices fall back from the GPU delegate to CPU, which can make tracking less smooth.
- iOS may suspend audio when the tab is backgrounded; tap **Test sound** to wake it.
- There is no saved state. Reloading the page clears the strings.

## License

MIT License

Copyright (c) 2026 Blake Brannon

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
