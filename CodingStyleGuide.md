<center> <h1>Neumont College Game Studios</h1> </center>
<center> <h1>C++ Coding Style Guideline</h1> </center>

</p>

These coding guidelines focus on the C++- language and act as a general guide for other coding languages that are used at the studio.

## Introduction

The purpose of this style guide is to unify the formatting and style of all projects within the game studio. A common style is beneficial because it helps team members to read code that is common and retain a concise format throughout all projects. Many software companies enforce a coding standard that must be adhered to and getting exposure to a style guide helps students to be familiar with one.
Some of style choices made are well motivated and common to many companies while other choices are arbitrary. One style may not have an advantage over another but a choice was made to retain a consistent style. Some items may not be covered in this style guide and if so feel free to use whatever style you are accustomed to. The point of this document is not to have a coding war about the standards but to choose a direction and follow it. If there is something you would like to add or revise, please discuss it.

### Naming

The naming of functions, classes and variables is very important. The name should be clear and concise. Code is reading/writing is general done on a 10:1 ratio. So, making the code easy to read is vital.

* The bigger the scope of the name the more descriptive it should be.
  * Using common names for small loops is ok (I, j, k, …)
  * Do not use cryptic names or abbreviations
* Use correct American English spelling

### Variables

* Variable names should use the camel case format which is lowercase start and uppercase for each world in the name.
  * vertexColor, gameObject, worldPosition
* Member variables have m_ appended to the name. This allows member variables to be distinguished from local variables.
  * m_score, m_lives, m_timer
