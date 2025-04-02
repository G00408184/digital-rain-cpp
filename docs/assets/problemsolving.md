# Problem Solving

---
[🏠 Home](index.md) | [🎨 Design](design.md) | [🧠 Algorithm](algorithm.md) | [🐞 Debugging](problemsolving.md) | [🧠 Reflection](reflection.md)

## ❌ Character Glitches

Non-ASCII characters appeared (`?`), fixed by limiting the character set:

```cpp
const char charset[] = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz";
```

## 🖥️ Flicker Fix

Replaced `system("cls")` with cursor repositioning:

```cpp
SetConsoleCursorPosition(hConsole, { (SHORT)x, (SHORT)it->position });
```
