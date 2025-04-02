# 🐞 Problem Solving

---

[🏠 Home](index.md) | [🎨 Design](design.md) | [🧠 Algorithm](algorithm.md) | [🐞 Debugging](problemsolving.md) | [🧠 Reflection](reflection.md)

---

## ❌ Character Glitches

### 🔍 Problem:
At first, some characters were rendering as strange symbols (like `?`, `�`, etc.). This happened because the default `rand()` could return values that didn’t map to readable or printable ASCII characters.

### ✅ Solution:
I fixed this by creating a limited, clean character set using only alphanumeric characters. That ensured all generated characters would look visually consistent in the console.

```cpp
const char charset[] = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz";
return charset[rand() % (sizeof(charset) - 1)];
```

This completely removed the weird symbols and made the falling rain look more realistic and readable.

---

## 💻 Flicker Fix

### 🔍 Problem:
Originally, I used `system("cls")` to clear the screen each frame, but this caused constant flickering and performance issues.

### ✅ Solution:
I replaced it with `SetConsoleCursorPosition()` from the Windows API. Instead of clearing the entire screen, this simply moves the cursor to the location of each character and overwrites it — resulting in smooth rendering.

```cpp
SetConsoleCursorPosition(hConsole, { (SHORT)x, (SHORT)it->position });
std::cout << dc.value;
```

This small change made the animation look way more stable and fluid.

---

## 🧱 Drop Overlap & Life Management

### 🔍 Problem:
Sometimes drops would overlap, or stay on screen forever if not cleared properly.

### ✅ Solution:
To fix that, I added a `life` property to each `DropChar`. On every frame, the drop moves down and its life is reduced. When `life <= 0`, it's removed from the list safely during iteration.

```cpp
if (it->life <= 0 || it->position >= consoleHeight) {
    it = columns[x].erase(it); // Safe in-place erase using list iterator
} else {
    ++it;
}
```

This kept the screen clean and let the animation loop without getting cluttered or buggy.

---

## 📐 Console Resize Bugs

### 🔍 Problem:
If the console was resized while running, the layout would break and characters would start overlapping or disappear.

### ✅ Solution:
I detected console width and height dynamically each frame and reallocated the grid if it changed:

```cpp
GetConsoleScreenBufferInfo(hConsole, &csbi);
int newWidth = csbi.srWindow.Right - csbi.srWindow.Left + 1;
int newHeight = csbi.srWindow.Bottom - csbi.srWindow.Top + 1;

if (newWidth != consoleWidth || newHeight != consoleHeight) {
    consoleWidth = newWidth;
    consoleHeight = newHeight;
    columns = std::vector<std::list<DropChar>>(consoleWidth); // Reset columns
}
```

This made it much more robust — the rain now adjusts automatically if I resize the window!

---

## 💡 Summary

Debugging this project taught me a lot about console behavior, rendering performance, and clean real-time logic. Most bugs were solved by simplifying logic, choosing better data structures (like `std::list`), or using low-level API features like cursor control instead of hacks like `cls`.

It was honestly fun to fix things because I could instantly see the difference visually in the animation. 🙂
