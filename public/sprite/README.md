# Merry Neon Gremlin Sprite

A hand-constructed 64×128 Canvas sprite based on Merry's cartoon reference. The source image is **not** embedded, filtered, or traced. Every visible mark is generated from a named limited palette and editable integer rectangles.

## Files

- `neon-gremlin-sprite.html` — self-contained sprite lab with enlarged and native-size previews, scale control, alternate pose, palette, pixel data, and frame architecture.
- `neon-gremlin-widget.js` — drop-in transparent webpage creature. It walks along the viewport floor, turns at edges, occasionally dances/glitches, and dances when clicked.

Open `neon-gremlin-sprite.html` directly in a browser to inspect the artwork and controls. Keep the JavaScript file beside it to also see the small roaming website version.

## Put her on AstralTrash

Once the file is served from the site, add this just before `</body>`:

```html
<script src="/sprite/neon-gremlin-widget.js"></script>
```

The widget creates its own transparent fixed Canvas. It uses `pointer-events: none`, so it does not block buttons or links. A document-level hit test detects clicks on her bounding box without canceling the underlying page click.

The roaming widget defaults to native 64×128 so it stays small on a busy page. To enlarge it without blurring, set an integer `data-scale` from 1–3 on the loader:

```html
<script data-scale="2" src="/sprite/neon-gremlin-widget.js"></script>
```

## Tiny control API

```js
window.MerrySprite.dance();          // trigger a 2.4-second dance/glitch
window.MerrySprite.setMotion(false); // park her in place
window.MerrySprite.setMotion(true);  // resume wandering
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
