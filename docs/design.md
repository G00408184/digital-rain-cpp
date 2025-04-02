# Design & Test

---
[🏠 Home](index.md) | [🎨 Design](design.md) | [🧠 Algorithm](algorithm.md) | [🐞 Debugging](problemsolving.md) | [🧠 Reflection](reflection.md)

## 🧱 Architecture Overview

The project is composed of 3 classes:
- `DigitalRain`: Manages the animation loop and rendering
- `DropChar`: A struct for each falling character (value, color, lifespan)
- `CharacterStream`: Generates random characters

## 🧪 Testing Strategy

- Manual console resizing
- Keyboard exit using `_kbhit()`
- Visual inspection of fading, motion, and spacing
