# 🧠 Reflection & Modern C++

## 📚 Learning Journey

Working on the Digital Rain project was honestly one of the most fun coding tasks I've done. It really helped me understand how real-time animations work in the console and gave me a better grasp of how to structure a C++ program using modern techniques. Seeing the characters fall and fade in real time felt really satisfying.

## 🧰 Modern C++ Practices Used

- **Object-Oriented Design**: Classes like `DigitalRain` and `CharacterStream` encapsulate logic and allow for reuse and modular design.
- **Standard Library Containers**: Used `std::vector` and `std::list` to manage dynamic character streams and enable efficient insert/delete.
- **Scoped Initialization**: Used `{}` initialization, `auto`, and RAII principles.
- **Randomization & Seeding**: Used `srand(static_cast<unsigned int>(time(nullptr)))` to ensure randomness across runs.

## 💬 What I Learned

- Efficient rendering without flickering requires precise cursor control and selective redrawing.
- Managing lifecycles of visual elements (drops) introduces game loop logic in a console app.
- MkDocs is a powerful tool for documenting C++ projects and aligns well with GitHub Pages deployment.

## 🔮 Future Iteration

- Use `std::chrono` and C++20 coroutines for smoother frame management.
- Integrate user interactivity (pause, speed control).
- Explore Unicode support for more authentic glyphs.

---

[🏠 Home](index.md) | [🎨 Design](design.md) | [🧠 Algorithm](algorithm.md) | [🐞 Debugging](problemsolving.md) | [🧠 Reflection](reflection.md)
