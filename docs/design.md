# 🎨 Design & Test

---

[🏠 Home](index.md) | [🎨 Design](design.md) | [🧠 Algorithm](algorithm.md) | [🐞 Debugging](problemsolving.md) | [🧠 Reflection](reflection.md)

---

## 🧱 Architecture Overview

The program is designed with 3 main components:

- `DigitalRain`: Manages the animation loop, frame timing, and rendering logic.
- `DropChar`: Struct representing a falling character with position, lifespan, value, and color.
- `CharacterStream`: Utility class that generates randomized alphanumeric characters.

---

## 📦 Object Relationships

- `DigitalRain` contains a vector of `std::list<DropChar>` — each representing a vertical column.
- Characters are spawned, updated, and rendered via this structure.
- `CharacterStream` is only called during creation of new drops.

---

## ✅ Testing Strategy

- 🖥️ **Manual Resizing**: Console window is resized to test dynamic column adaptation.
- 🧪 **Keyboard Input**: Exit tested using `_kbhit()` for clean shutdown.
- 👁️ **Visual Tests**:
  - Ensured proper fading, drop speed, and color dimming.
  - Verified characters did not overlap or "stick".
- 🔁 **Frame Stability**: Tested with varying frame delays (Sleep values).

---

## 🧠 Key Design Choices

- ❌ Avoided full screen clearing to reduce flicker (`system("cls")`).
- ✅ Used `SetConsoleCursorPosition()` for precision overwrite.
- ✅ Used `std::list` for fast removal of expired characters mid-loop.
- ✅ Colors and fade transitions were optimized using bitwise masking.

---

