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
- A 10% chance is used to control spawn frequency.

- Prevents drops from stacking unnaturally.

- Drop lifespan, position, and color are randomized
## 💡 Fading and Deletion

Characters fade as their `life` reduces. Below `life < 5`, intensity is dimmed.

```cpp
if (dc.life < 5) {
    color = dc.color & ~FOREGROUND_INTENSITY;
}
```

The animation is driven by a real-time loop in `DigitalRain::run()`:

```cpp
while (!_kbhit()) {
    update();
    render();
    Sleep(50); // Delay between frames
}
```
This loop:
- Continuously updates the state of all falling characters.
- Redraws only the necessary parts of the screen.
- Exits gracefully when a key is pressed using _kbhit().
