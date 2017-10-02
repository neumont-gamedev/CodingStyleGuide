<center> <h1>Neumont College Game Studios</h1> </center>
<center> <h1>C++ Coding Style Guideline</h1> </center>

These coding guidelines focus on the C++- language and act as a general guide for other coding languages that are used at the studio.

## Introduction

The purpose of this style guide is to unify the formatting and style of all projects within the game studio. A common style is beneficial because it helps team members to read code that is common and retain a concise format throughout all projects. Many software companies enforce a coding standard that must be adhered to and getting exposure to a style guide helps students to be familiar with one.
Some of style choices made are well motivated and common to many companies while other choices are arbitrary. One style may not have an advantage over another but a choice was made to retain a consistent style. Some items may not be covered in this style guide and if so feel free to use whatever style you are accustomed to. The point of this document is not to have a coding war about the standards but to choose a direction and follow it. If there is something you would like to add or revise, please discuss it.

## Naming

The naming of functions, classes and variables is very important. The name should be clear and concise. Code is reading/writing is general done on a 10:1 ratio. So, making the code easy to read is vital.

* The bigger the scope of the name the more descriptive it should be.
  * Using common letters for small loops is ok (I, j, k, …)
* Do not use cryptic names or abbreviations
* Use correct American English spelling
* Make names pronounceable
* Use names that are searchable
* Use complement names and be consistent with their usage
  * If you use Start/Stop in your code then use those names throughout, do not use Begin/End if already declared Start/Stop
  * get/set, add/remove, create/destroy, start/stop, insert/remove, increment/decrement, begin/end, first/last, up/down, min/max, next/previous, old/new, open/close, show/hide, suspend/resume, initialize/shutdown

### Variables
* Variables should be in the form of a noun
  * player, enemy, projectile 
* Variable names should use camel case format which is lowercase start and uppercase for each word in the name.
  * vertexColor, gameObject, worldPosition
* Class member variables should have m_ prefixed to the name. This allows member variables to be distinguished from local variables.
  * m_score, m_lives, m_timer
  * Public member variables of structs do not require m_
* Static member variables should have a s_ prefix
* Global member variables should have a g_ prefix
* Only one variable should be listed per line/declaration
  * int score;
  * float speed;
* When declaring boolean variables use the term “is” or “has” in front of the name
  * isActive, isInitialized

### Functions

* Functions should be in the form of verb or verb/noun
* Function names should use pascal case which is uppercase start and uppercase for each word in the name.
  * GetScore, SetPlayerName
* Avoid verbs that are ambiguous (Handle, Process,…)
* Functions that return a Boolean value should ask a true/false question
  * bool IsVisible()

### Classes/Structs
* Class/Struct names should be in the form of a noun
* Class/Struct names should use pascal case which is uppercase start and uppercase for each word in the name.
  * GamePlayer, AudioManager, EnemyWeapon, VertexFormat

### Enum
* Enum should be prefixed with an ‘e’
  * enum eState
  * enum eVertexFormat
* Values declared in the enum should be all capitals with an underscore between names
  * ACTIVE, LASER_WEAPON

### Macros
* Macros should be all capitals with an underscore between names
  * #define PACK_RGB(r, g, b)

## Comments
Comments are important to help the reader understand the code if it is complex or needs extra information to use. Comments tend to diverge from the original code because the comment is not updated when the code is changed. Therefore, it is vital that the code should be self-explanatory.
* Use // for descriptive comments and /* to disable code
* Do not leave old disabled code in the source
  * Code that is disabled makes it harder to remember why it was commented out in the first place
  * With source control disabled code can be found in the history of the file
* Write self-documenting code
  * playerHealth = playerHealth – damage;
* Do not comment bad code. Take the time to correct the code
  * // this is totally messed up but it works most of the time - fix me 

## Structs / Class
Use structs for passive objects that carry data. Do not have structs that contain function methods.

## Variables

* Avoid global variables
* Avoid variables in the global namespace
  * Use a namespace to contain a variable
  * Do not pollute the global namespace with variables

## Functions
Functions should be small and do only one thing. If the function is long or does multiple actions, break the function into smaller functions. Keep them short and simple.

* Avoid functions in the global namespace
  * Use a namespace to encapsulate a function
  * Do not pollute the global namespace with functions
* The order of parameters to a function should be: inputs then outputs
  * Some parameters may be considered as both input and output
  * You may have to bend this rule
* Avoid have long parameter lists
  * Consider grouping the data in a struct if there is multiple related data
* Pass large data to a function as a reference unless a null pointer is possible
  * void DamageGameObject(GameObject& gameObject, Weapon& weapon);
* Strive to use the const keyword when applicable
  * If a method does not modify the object use const
    * float GetHealth() const { return m_health; }
  * If a function parameter is not altered in the function use const
    * bool IsPlayerAlive(const Player& player) { return player.GetHealth() <= 0.0f; }

## Spacing/Indentation/Bracing

### Spacing

* Put a space between if, for, while and the parenthesis that follows.
  * If (x >= 5.0f)
  * for (int I = I < 5; i++)
* Do not put a space between the function name and the parenthesis in a function call.
  * void CreateEnemy(); 
* Do not put spaces inside parenthesis.
* Put spaces after commas, do not put spaces before commas.
  * GetGameObjectType(objects, eType.ENEMY, true);
* Place the pointer and reference symbol with the type and not the variable
  * GamePlayer* player;
  * bool IsEnemyInRange(const Enemy& enemy, float distance);

### Indentation

* Use tabs not spaces
  * Use tabs that are equal to 4 spaces

### Bracing
Each company and developer has their own style when it comes to the placing of braces. The objective of this guide is to have a consistent style that will be familiar to all readers.
* All braces should exist on their own line
  * If (isActive) </br>
{ </br>
	    return; </br>
} </br>


## .h / .cpp Files
### .h
Header files can become tricky and result in a tangled mess of errors resulting from .h files with circular dependencies. Following the guidelines below will help manage the header dependencies.

* Use #pragma once at the top of the file, do not use include guard #ifndef/#define/#endif
  * All modern compilers support #pragma once 
* Use forward declarations when possible
  * Avoid using #include in a header file that is not required
* Avoid function implementations in header files, prefer headers with declarations only
* Avoid having multiple classes in the same header unless they are nested in another class or short classes
* Include third party headers with #include <name>
  * Third party header locations should be provided through the build script

### .cpp
Classes should not be split across multiple .cpp files.

## Conclusion
It is the intent of this document to come up with a good standard that is followed by all students of the game programming degree. The desire is to have the students write clean, clear and well formatted code.

**CLARITY IS KING!**

* Do not try to write complex code, simplicity is best
* The point of good code is to be clear not clever

Much of this document was created from personal experience and from the references listed below. It is the hope that this guide follows many of the same standards that are used in the industry today.

https://google.github.io/styleguide/cppguide.html
https://docs.unrealengine.com/latest/INT/Programming/Development/CodingStandard/
http://docs.cryengine.com/pages/viewpage.action?pageId=25530454
http://fd.fabiensanglard.net/doom3/CodeStyleConventions.pdf
https://github.com/niklasfrykholm/blog/blob/master/reference/coding-style.md


