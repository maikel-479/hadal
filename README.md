<div align="center">

# Hadal 

A deep-sea inspired theme set for [Zed](https://zed.dev), currently with two dark variants: Hadal Deep and Hadal Midnight.

| Hadal Deep | Hadal Midnight |
|------------|----------------|
|![Hadal Deep](assets/Hadal_Deep.png)|*Screenshot coming — capture with the dev extension and save as `assets/Hadal_Midnight.png`*|
  
![extension installation counts](https://zedbadge.dev/extension/hadal-theme.svg)

</div>

## Features

- **Two dark variants** — Hadal Deep and Hadal Midnight, 187 style keys each with full parity
- **105 syntax captures** — comprehensive coverage of all syntax elements
- **16 terminal ANSI colors** — plus bright and dim variants for the integrated terminal
- **8 player colors** — for collaboration cursors
- **Vim mode support** — complete color definitions for all vim modes
- **Version control integration** — conflict markers, diff colors, and status indicators

## Install

### From the Zed extension store

1. Open Zed
2. `Cmd` `Shift` `P` → **zed: extensions**
3. Search for **Hadal**
4. Click **Install**

### As a dev extension

```sh
git clone https://github.com/maikel-479/hadal.git
```

1. In Zed: `Cmd` `Shift` `P` → **zed: install dev extension**
2. Select the cloned directory
3. `Cmd` `Shift` `P` → **theme selector: toggle** → pick **Hadal Deep**

## Switching

`Cmd` `K` `Cmd` `T` opens the theme selector, or `Cmd` `Shift` `P` →
**theme selector: toggle**.

To pin a variant, edit `settings.json`:

```json
{
  "theme": "Hadal Deep"
}
```

Or set Midnight instead:

```json
{
  "theme": "Hadal Midnight"
}
```

## License

[MIT](LICENSE)

---

Built by [@maikel-479](https://github.com/maikel-479).
