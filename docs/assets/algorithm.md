# Algorithm Details

---
[🏠 Home](index.md) | [🎨 Design](design.md) | [🧠 Algorithm](algorithm.md) | [🐞 Debugging](problemsolving.md) | [🧠 Reflection](reflection.md)

## 🎲 Random Drop Creation

Each column has a 10% chance to create a new drop per frame if it’s empty.

```cpp
if (rand() % 100 < 10 && columns[x].empty()) {
    createNewDrop(x);
}
```

## 💡 Fading and Deletion

Characters fade as their `life` reduces. Below `life < 5`, intensity is dimmed.

```cpp
if (dc.life < 5) {
    color = dc.color & ~FOREGROUND_INTENSITY;
}
```
