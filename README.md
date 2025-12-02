# Windmill Studios - Coding Style

This repository contains the official coding style configuration, naming conventions, and formatting rules used across all **Windmill Studios** projects (Mistral Engine, Vendaval Editor, Floresta, etc.).

The goal is to maintain a clean, readable, and consistent codebase across all repositories.

## 🛠️ Tools & Configuration

### Clang-Format
We use **clang-format** to automate visual styling (indentation, spacing, braces).
* The official configuration file is located at the root of this repository: [.clang-format](.clang-format).
* All IDEs (CLion, VS Code, Visual Studio) must be configured to use this file.

### CMake Integration
To ensure your project always uses the latest version of this standard, add the following to your main `CMakeLists.txt`:

```cmake
set(STYLE_URL "https://raw.githubusercontent.com/WindmillStudios/Coding-Style/refs/heads/main/.clang-format")
set(LOCAL_STYLE_FILE "${CMAKE_CURRENT_LIST_DIR}/.clang-format")

file(DOWNLOAD "${STYLE_URL}" "${LOCAL_STYLE_FILE}" SHOW_PROGRESS)
```

## 📏 Naming Conventions

| Element                 | Style        | Prefix/Suffix | Example                               |
|:------------------------|:-------------|:--------------|:--------------------------------------|
| **Namespaces**          | `PascalCase` | None          | `Mistral`, `Vendaval`                 |
| **Classes / Structs**   | `PascalCase` | None          | `Component`, `RenderPipeline`         |
| **Methods / Functions** | `PascalCase` | None          | `StartApplication()`, `GetChild()`    |
| **Member Variables**    | `PascalCase` | `m`           | `mId`, `mParent`, `mIsActive`         |
| **Local Variables**     | `camelCase`  | None          | `activeCamera`, `texturePath`         |
| **Parameters**          | `camelCase`  | None          | `const std::string& name`             |
| **Constants / Enums**   | `PascalCase` | None          | `Vec2::Zero`, `ResourceType::Texture` |
| **Macros**              | `UPPER_CASE` | None          | `LOG_NONE`, `MISTRAL_API`             |

## 📝 Coding Style & Formatting
### 1. Braces
   We use the Allman style (also known as BSD style). Opening braces must always be placed on a new line, both for function definitions and control blocks.

```c++
// ✅ Correct
void UpdateEvent()
{
    if (mIsActive)
    {
        DoSomething();
    }
    else
    {
        Sleep();
    }
}

// ❌ Incorrect
void UpdateEvent() {
    if (mIsActive) {
        DoSomething();
    }
}
```

### 2. Pointers and References
The asterisk * and ampersand & must be aligned with the type, not the variable name.


```c++
// ✅ Correct
Component* parent;
const std::string& GetName();

// ❌ Incorrect
Component *parent;
const std::string &GetName();
```

### 3. Private Members
Class member variables must always be private or protected and start with m. Public access should be provided via Getters and Setters.

```c++
class Player
{
public:
    void SetHealth(float health) { mHealth = health; }
    float GetHealth() const { return mHealth; }

private:
    float mHealth; // ✅ Correct
    // float health; ❌ Incorrect
    // float _health; ❌ Incorrect
};
```

### 4. Includes
- Use quotes `""` for local project files.
- Use angle brackets `<>` for system libraries or external dependencies (including the Mistral library itself when used externally).

```c++
#include "Component.h"       // Local
#include <Mistral/Mistral.h> // External Library / Core
#include <vector>            // Standard Library
```

## ✨ Modern C++ (C++20)
We encourage the usage of modern C++ features to improve safety and performance.

- `[[nodiscard]]`: Use it on functions that return important values (getters, factory functions).

- `std::unique_ptr` / `std::shared_ptr:` Avoid raw `new` and `delete` for memory ownership.

- `auto`: Use it when the type is obvious (e.g., iterators or explicit casts), but prefer explicit types if it aids readability.

- `nullptr`: Never use `NULL`.

## 📄 File Structure
- Header files (`.h`) must use `#pragma once` to prevent multiple inclusions.

- Clear separation between declaration (`.h`) in `include/` folders and implementation (`.cpp`) in `src/` folders for libraries.

---

© 2025 Agustín Molina Uasuf - Windmill Studios