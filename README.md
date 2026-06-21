# Neumont Game Studios

# C++ Coding Style Guide

These coding guidelines focus on modern C++ and serve as a general reference for software development within Neumont Game Studios. The purpose of this document is not to enforce arbitrary rules, but to encourage consistency, readability, and maintainability across all projects.

---

# Introduction

A coding standard helps developers work together more effectively by making code easier to read, understand, and maintain. Most professional software studios follow established coding standards, and exposure to these practices prepares students for industry expectations.

While many style choices are subjective, consistency is more important than the specific choice itself. This guide establishes a common direction for projects developed within the studio.

When in doubt, prioritize clarity over cleverness.

---

# General Principles

## Clarity is King

Code is read far more often than it is written. Write code that is easy for another developer to understand.

Good:

```cpp
playerHealth -= damage;
```

Bad:

```cpp
hp -= dmg;
```

unless the shorter names are widely understood within the context.

## Prefer Simplicity

Write the simplest solution that solves the problem.

Avoid:

* Unnecessary abstraction
* Premature optimization
* Clever but difficult-to-read code

## Consistency Matters

Follow existing naming and design conventions throughout a project.

If a project uses:

```cpp
StartGame();
StopGame();
```

do not introduce:

```cpp
BeginGame();
EndGame();
```

for the same concepts.

---

# Naming

Names should be clear, descriptive, searchable, and pronounceable.

## General Rules

* Use correct American English spelling.
* Avoid cryptic abbreviations.
* Use descriptive names for large-scope objects.
* Single-letter names are acceptable only for small loop counters.
* Use complementary naming pairs consistently:

  * Start / Stop
  * Create / Destroy
  * Add / Remove
  * Show / Hide
  * Open / Close
  * Begin / End
  * Enable / Disable

---

# Variables

Variables should be nouns or noun phrases.

## Local Variables

Use camelCase.

```cpp
int score;
float movementSpeed;
Vector2 worldPosition;
```

## Member Variables

Prefix member variables with `m_`.

```cpp
class Player
{
private:
    int m_health;
    float m_speed;
};
```

## Static Member Variables

Prefix static member variables with `s_`.

```cpp
static int s_instanceCount;
```

## Global Variables

Avoid global variables whenever possible.

If shared data is required, prefer namespaces over global namespace variables.

```cpp
namespace Game
{
    extern PlayerManager playerManager;
}
```

## Boolean Variables

Boolean variables should read naturally in conditional statements.

```cpp
bool isActive;
bool hasWeapon;
bool canJump;
bool shouldRespawn;
bool wasDestroyed;
```

Examples:

```cpp
if (canJump)
{
}

if (hasWeapon)
{
}
```

---

# Functions

Functions should perform one task and do it well.

## Naming

Functions should use PascalCase and be written as verbs or verb phrases.

```cpp
GetHealth();
SetPosition();
CreateEnemy();
LoadTexture();
```

Avoid vague names such as:

```cpp
Process();
Handle();
Manage();
DoStuff();
```

## Boolean Functions

Boolean-returning functions should ask a question.

```cpp
bool IsAlive() const;
bool HasAmmo() const;
bool CanAttack() const;
```

## Function Parameters

Order parameters as:

1. Inputs
2. Outputs

Example:

```cpp
bool IntersectRay(
    const Ray& ray,
    const Collider& collider,
    HitInfo& hitInfo);
```

Avoid long parameter lists. If several parameters represent related data, consider grouping them into a struct or class.

---

# Classes and Structs

## Classes

Use classes when encapsulating behavior and state.

Class names should use PascalCase.

```cpp
class AudioManager;
class EnemySpawner;
class PhysicsWorld;
```

## Structs

Use structs primarily for passive data objects.

```cpp
struct Vertex
{
    Vector3 position;
    Vector2 uv;
};
```

Small helper functions are acceptable, but structs should primarily represent data rather than behavior.

---

# Enumerations

Use scoped enumerations (`enum class`).

Enumeration names and values should use PascalCase.

```cpp
enum class WeaponType
{
    Laser,
    Rocket,
    Plasma
};
```

Usage:

```cpp
WeaponType weapon = WeaponType::Laser;
```

Scoped enumerations improve type safety and prevent namespace pollution.

---

# Constants

Prefer `constexpr` whenever possible.

```cpp
constexpr float MaxSpeed = 250.0f;
constexpr int MaxPlayers = 4;
```

Use PascalCase for constant names.

Avoid macros for constants.

---

# References and Pointers

Understanding when to use references and pointers is essential for writing clear and maintainable C++ code.

## General Rule

Prefer references over pointers whenever a valid object is required.

A reference indicates that an object must exist and cannot be null.

```cpp
void DamagePlayer(Player& player)
{
    player.TakeDamage(10);
}
```

Use pointers when an object may not exist.

```cpp
void SetTarget(Enemy* target)
{
    m_target = target;
}
```

A null pointer represents the absence of an object.

```cpp
if (m_target != nullptr)
{
    m_target->Attack();
}
```

## Function Parameters

### Required Object

Use a reference.

```cpp
void Render(Sprite& sprite);
```

Use a const reference when modification is not required.

```cpp
void Render(const Sprite& sprite);
```

### Optional Object

Use a pointer.

```cpp
void SetOwner(Player* owner);
```

The pointer may be nullptr to indicate no owner.

## Passing Large Objects

Pass large objects as const references.

Good:

```cpp
void Render(const Mesh& mesh);
void LoadLevel(const LevelData& levelData);
```

Avoid:

```cpp
void Render(Mesh mesh);
```

which creates an unnecessary copy.

## Output Parameters

Output parameters should generally be references.

```cpp
bool Raycast(
    const Ray& ray,
    HitInfo& hitInfo);
```

## Reference Members

Avoid storing references as class members.

Bad:

```cpp
class Player
{
private:
    Renderer& m_renderer;
};
```

References cannot be reseated and often complicate lifetime management.

Prefer pointers for non-owning member relationships.

```cpp
class Player
{
private:
    Renderer* m_renderer;
};
```

---

# Memory Management

Prefer modern memory management techniques.

## Ownership

Use `std::unique_ptr` for exclusive ownership.

```cpp
std::unique_ptr<Player>
```

Example:

```cpp
class Scene
{
private:
    std::vector<std::unique_ptr<GameObject>> m_objects;
};
```

Use `std::shared_ptr` only when ownership must be shared.

```cpp
std::shared_ptr<Texture>
```

Avoid using shared ownership by default.

## Raw Pointers

Raw pointers should generally represent non-owning references to objects.

```cpp
Enemy* m_target;
```

The object is owned elsewhere.

---

# Standard Library

Prefer standard library containers and utilities before creating custom solutions.

Commonly used types:

```cpp
std::vector
std::array
std::unordered_map
std::string
std::optional
```

Do not reinvent functionality already provided by the standard library unless there is a compelling reason.

---

# Modern C++ Guidelines

## Use nullptr

Good:

```cpp
Player* player = nullptr;
```

Bad:

```cpp
Player* player = NULL;
```

---

## Prefer using Over typedef

Good:

```cpp
using EntityId = uint32_t;
```

Bad:

```cpp
typedef uint32_t EntityId;
```

---

## Use Range-Based Loops

Good:

```cpp
for (auto& enemy : enemies)
{
    enemy.Update();
}
```

---

## Use auto When the Type Is Obvious

Good:

```cpp
auto player = std::make_unique<Player>();
```

Avoid:

```cpp
auto value = SomeComplicatedFunction();
```

when the type is unclear.

---

# Const Correctness

Use `const` whenever possible.

## Member Functions

If a member function does not modify the object, mark it const.

```cpp
float GetHealth() const;
```

## Parameters

Pass read-only objects as const references.

```cpp
void Render(const Camera& camera);
```

Const correctness communicates intent and helps prevent bugs.

---

# Comments

Comments should explain why, not what.

Good:

```cpp
// Enemy remains invulnerable for a brief period
// after spawning to prevent unfair deaths.
```

Avoid:

```cpp
// Increase score by 10.
score += 10;
```

The code already explains what it does.

## Guidelines

* Use `//` for comments.
* Remove obsolete comments.
* Do not leave large blocks of disabled code.
* Use source control history instead.

---

# Spacing and Formatting

## Spacing

Place a space after control statements.

```cpp
if (isAlive)
```

```cpp
for (int i = 0; i < 10; i++)
```

Do not place spaces inside parentheses.

```cpp
MovePlayer(player, speed);
```

Place spaces after commas.

```cpp
SpawnEnemy(position, rotation, speed);
```

## Pointers and References

Associate pointers and references with the type.

```cpp
Player* player;
const Enemy& enemy;
```

Not:

```cpp
Player *player;
Enemy &enemy;
```

---

# Indentation

Use tabs.

A tab should be displayed as four spaces.

---

# Braces

Opening braces should appear on their own line.

```cpp
if (isActive)
{
    Update();
}
```

```cpp
class Player
{
public:
    void Update();
};
```

Always use braces, even for single-line conditionals.

Good:

```cpp
if (isAlive)
{
    Respawn();
}
```

Avoid:

```cpp
if (isAlive)
    Respawn();
```

---

# File Organization

## Header Files (.h)

* Use `#pragma once`
* Prefer forward declarations where possible
* Minimize includes
* One major class per header
* Avoid function implementations in headers unless required

Example:

```cpp
#pragma once

class Renderer;

class Player
{
};
```

## Source Files (.cpp)

Classes should not be split across multiple source files.

Recommended order:

1. Includes
2. Constants
3. Enumerations
4. Structs
5. Class implementation

---

# Class Layout

Recommended class organization:

```cpp
class Player
{
public:
    Player();

    void Update();
    void Render();

protected:

private:
    void ProcessInput();

private:
    int m_health;
    float m_speed;
};
```

Group related functionality together and keep public interfaces concise.

---

# Namespaces

Avoid placing functions and variables directly into the global namespace.

Good:

```cpp
namespace Physics
{
    void Simulate();
}
```

Bad:

```cpp
void Simulate();
```

Namespaces help organize code and reduce naming conflicts.

---

# AI-Assisted Development

AI tools can be useful development assistants, but they do not replace understanding.

Students are responsible for all code submitted regardless of whether it was written by:

* The student
* Another developer
* An AI tool

If you cannot explain how a piece of code works, you should not submit it.

AI-generated code should be reviewed, understood, tested, and integrated thoughtfully.

---

# Conclusion

The goal of this guide is not to create perfect code. The goal is to create code that is easy to read, easy to maintain, and easy to extend.

**CLARITY IS KING**

* Write code for humans first.
* Prefer simple solutions.
* Favor readability over cleverness.
* Consistency is more important than personal preference.

The best code is not the most impressive code—it is the code that another developer can understand six months later.
