# Merry Neon Gremlin Sprite

A hand-constructed 64×128 Canvas sprite based on Merry's cartoon reference. The source image is **not** embedded, filtered, or traced. Every visible mark is generated from a named limited palette and editable integer rectangles.

## Files

- `neon-gremlin-sprite.html` — self-contained sprite lab with enlarged and native-size previews, scale control, alternate pose, palette, pixel data, and frame architecture.
- `neon-gremlin-widget.js` — drop-in transparent homepage character. It anchors beside the AstralTrash title, dances continuously in place, shuffles its feet independently, and adds extra glitches when clicked.

Open `neon-gremlin-sprite.html` directly in a browser to inspect the artwork and controls. Keep the JavaScript file beside it to also see the in-place dancing demo.

## Put her on AstralTrash

Once the file is served from the site, add this just before `</body>`:

```html
<script src="/sprite/neon-gremlin-widget.js"></script>
```

The widget finds the HOME-page `AstralTrash` heading and pins its transparent Canvas to that hero section's measured coordinates. The Canvas stays outside React's managed DOM, so tab changes cannot accidentally delete it. It hides automatically when the title is absent on another section. It uses `pointer-events: none`, so it does not block buttons or links. A document-level hit test detects clicks on her bounding box without canceling the underlying page click.

The roaming widget defaults to native 64×128 so it stays small on a busy page. To enlarge it without blurring, set an integer `data-scale` from 1–3 on the loader:

```html
<script data-scale="2" src="/sprite/neon-gremlin-widget.js"></script>
```

## Tiny control API

```js
window.MerrySprite.dance();          // intensify the dance/glitch for 2.4 seconds
window.MerrySprite.setMotion(false); // freeze her in place
window.MerrySprite.setMotion(true);  // resume dancing
window.MerrySprite.destroy();        // remove sprite and listeners
```

`prefers-reduced-motion: reduce` automatically parks her and changes a click into one quick blink.

## Editing and future sprite sheets

`PALETTE` contains the reusable colors. `PARTS` contains rectangles in the format:

```js
[colorName, x, y, width, height]
```

Frames offset named body groups and add overlays. The current named frames are `idle`, `walkA`, `walkB`, `blink`, `danceLeft`, `danceRight`, and `glitch`. Future states such as `jump`, `wave`, `sit`, `sleep`, and `surprised` can follow the same structure.

To export a conventional sprite sheet later, draw each frame into adjacent 64×128 cells on a second Canvas and export that Canvas as PNG. The runtime can continue using the coordinate data or switch to the sheet.
