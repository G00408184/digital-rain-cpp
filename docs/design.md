# 🎨 Design & Test

---

[🏠 Home](index.md) | [🎨 Design](design.md) | [🧠 Algorithm](algorithm.md) | [🐞 Debugging](problemsolving.md) | [🧠 Reflection](reflection.md)

---

## 🧱 Architecture Overview

The project is built using modern C++ and is structured around three main components:

- `DigitalRain`: Controls the main animation loop, frame updates, console state, and rendering.
- `DropChar`: A struct that holds information for a single falling character (position, life, value, color).
- `CharacterStream`: A helper class that provides randomized alphanumeric characters for display.

### `DropChar` Structure

```cpp
struct DropChar {
    int position;   // Vertical Y position
    int life;       // Remaining lifespan
    char value;     // Character to render
    WORD color;     // Console text color
};
```

---

## 📦 Object Relationships

The main simulation is built around a vertical column structure:

- `std::vector<std::list<DropChar>> columns`: each vector index corresponds to a column on screen.
- Each `DropChar` in the list is a character that is falling in that column.
- Characters are created, updated, and erased in real-time.

```cpp
std::vector<std::list<DropChar>> columns;
```

Characters are spawned via:

```cpp
createNewDrop(x);
```

Where `x` is the column index and the new drop is added at the top.

---

## ✅ Testing Strategy

Testing was done through both code-driven validation and visual inspection.

### 🖥️ Manual Console Resizing

- Console width and height are detected using:

```cpp
GetConsoleScreenBufferInfo(hConsole, &csbi);
```

- If dimensions change, the column layout is reinitialized:

```cpp
if (newWidth != consoleWidth || newHeight != consoleHeight) {
    consoleWidth = newWidth;
    consoleHeight = newHeight;
    columns = std::vector<std::list<DropChar>>(consoleWidth);
}
```

### 🧪 Keyboard Exit

- Used `_kbhit()` to detect key presses for clean exit during runtime.

```cpp
while (!_kbhit()) {
    update();
    render();
    Sleep(50);
}
```

### 👁️ Visual Inspection

- Ensured proper behavior:
  - Characters move smoothly
  - Drops fade and disappear over time
  - No overlapping glitches
- Fading check using bitwise logic:

```cpp
if (dc.life < 5) {
    color = dc.color & ~FOREGROUND_INTENSITY;
}
```

---

## 🧠 Key Design Choices

### 🟢 Efficient Console Rendering

- ❌ Avoided `system("cls")` because it causes flicker and screen tear.
- ✅ Used `SetConsoleCursorPosition()` for precise, fast updates:

```cpp
SetConsoleCursorPosition(hConsole, { (SHORT)x, (SHORT)dc.position });
std::cout << dc.value;
```

### 🟢 Fade Effect Using Bitmask

- Bitwise logic was used to dim colors when drops are nearly expired:

```cpp
color = dc.color & ~FOREGROUND_INTENSITY;
```

### 🟢 Smart Data Structures

- `std::list` allows for safe in-loop erasure of expired characters:

```cpp
if (it->life <= 0 || it->position >= consoleHeight) {
    it = columns[x].erase(it);
}
```

- `std::vector` gives O(1) access per column and is resized dynamically.

### 🟢 Modular & Reusable

- All logic is encapsulated in methods (`initialize`, `update`, `render`, `cleanup`).
- Clean separation of logic (animation vs. rendering vs. data).

---

## 📌 Summary

This project uses modern C++ to create a visually engaging animation inside the Windows console.  
Using the Windows API directly (rather than libraries or screen clearing) results in a smoother, more responsive simulation.  
The architecture is modular, efficient, and well-suited for further expansion such as colored trails, sound, or input interaction.
