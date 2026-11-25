#### Note to user:

- If desired, RGB underglow must be manually enabled before building and flashing. Check 'helix.conf' to do so.
- Peripheral RGB function is impaired until full support is implemented in the master branch.
- OLED displays are not currently included in this shield. This will be updated after OLED support is live.
- 'KANA' and 'EISUU' input is currently utilized under the 'LANG1' and 'LANG2' keycodes respectively.

---

Thanks to Nicell, KemoNine, petejohanson, TJ "Chormbo The Great", joelspadin/Rinh, Wofiel, Okke, innovaker,
and the rest of the ZMK contributors for their support in constructing this shield. I appreciate your assistance greatly.
This has been a valuable learning experience for me. May this contribution serve the community well.

---

#### Standalone halves (Halfix)

Either half can be built as a standalone keyboard, with no split. These are separate shields, defined in
`boards/shields/halfix/`:

| Shield | PCB | Extra keys | Keyboard name |
|---|---|---|---|
| `halfix` | left half | right-most column | Halfix |
| `halfix_mirrored` | right half | left-most column | Halfix Mirrored |

```yaml
include:
  - board: nice_nano@2.0.0//zmk
    shield: halfix
  - board: nice_nano@2.0.0//zmk
    shield: halfix_mirrored
```

Both shields use `halfix.keymap`. Each physical layout lists the two inner extra keys last in rows 3 and 4, so a
key position means the same key on either half. To customize, put a `halfix.keymap` in your zmk-config. It
applies to both shields, and `felix.keymap` stays the split keymap.

Flash `settings_reset` when switching a half between split and standalone to clear old pairing data.

---

#### OLED display

The display is off by default, and its I2C and SSD1306 drivers aren't built. To enable it, add the `felix-display`
snippet to any Felix or Halfix build. It sets `CONFIG_ZMK_DISPLAY` and the built-in status screen:

```yaml
include:
  - board: nice_nano@2.0.0//zmk
    shield: felix_left
    snippet: felix-display
  - board: nice_nano@2.0.0//zmk
    shield: halfix
    snippet: felix-display
```

Outside GitHub Actions, use `west build ... -S felix-display`. Setting `CONFIG_ZMK_DISPLAY=y` in your zmk-config's
`felix.conf` (or `halfix.conf`) also works.
