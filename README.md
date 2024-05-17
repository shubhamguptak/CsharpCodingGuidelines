# C# Coding Guidelines

Last updated: 2024-05-16/Shubham

The guidelines in this document can be used by software development companies when developing software written in `C#`.

**NOTE**: Some of these guidelines are based on standard Microsoft C# guidelines and may not be totally relevant to your company's Unity development.


## Company copyright text
1. Add at the top of each script.
2. If the project spans multiple years, add the range - i.e., `2021-2024`. No spaces.
3. Update the copyright year only when a component is modified.
```sh
// Brief description of the purpose
//
// Copyright (C) {currentYear} Company name.
// All Rights Reserved.
```

## Layout conventions
1. One statement per line.
2. One declaration per line.
3. Line indent with one tab - four (4) spaces.
5. Use parentheses to make clauses in an expression more explicit.
6. A single blank line at the end of every file.


## Regions
1. Make use of regions to group related functionality together. Although regions are sometimes considered 'code smells', they can be useful to hide code while working within a file.
2. Ensure that regions are matched and named consistently - i.e., `#region Unity`, `#endregion Unity`.
3. Group base Unity methods together in `#region Unity` - i.e., `Awake()`, `Start()`, `OnEnable()`, `OnDisable()`.
4. Group `OnTrigger` methods together in `#region OnTrigger` - i.e., `OnTriggerEnter()`, `OnTriggerExit()`.
5. Group `OnCollision` methods together in `#region OnCollision` - i.e., `OnCollisionEnter()`, `OnCollisionStay()`.
6. Always add a blank line before _and_ after `#region` and `#endregion`.
7. Use your judgment for anything else, but follow the above pattern. If in doubt, ask...


## Comment conventions
1. Begin the comment text with an uppercase letter.
2. Write comments in **US English**, using punctuation where appropriate.
3. Comments should be free from typos and spelling mistakes.
4. Insert one space between the comment delimiter (//) and the comment text - i.e.,  `// This is a comment`
5. Do **not** end comments with a period (`.`).
6. Field comments `public String NewPublicField; // This is a String`
7. Ensure comments are adding value - i.e., are they stating something obvious about the code? Use the _why_, not _what_ - the code should speak for itself.
8. Ensure comments are accurate and relevant.

## Performance Considerations
1. Avoid Frequent Use of Find and GetComponent: These methods are costly. Cache component references during initialization if possible.
2. Minimize Use of Update: If a method doesn’t need to check conditions every frame, consider using FixedUpdate for physics-related updates or Coroutine for delayed execution.
3. Object Pooling: Instead of instantiating and destroying objects frequently (like bullets in a shooter game), use an object pooling system.

## Unity Specific Practices
1. Serialized Fields: Use [SerializeField] private fields instead of public fields unless absolutely necessary to keep encapsulation intact while still exposing fields to the Unity Editor.
2. Event Functions: Leverage Unity's built-in event functions like Awake, Start, Update, FixedUpdate, etc., wisely.
3. Use Unity’s Data Types and Structures: Prefer Unity-specific structures like Vector3, Quaternion, etc., for better integration and performance.

## Modular Design
1. Component-Based Design: Decompose features into smaller, reusable components to make it easier to manage and update them.
2. Single Responsibility Principle: Each class or component should have one reason to change, meaning it should only have one job or responsibility.
3. Component Reusability: Design prefabs to be as modular as possible. This allows you to mix and match components to create variations without duplicating the entire prefab.
4. Prefab Variants: Use prefab variants to create different versions of a base prefab. This is useful for creating different types of a base model, such as enemies with varying abilities or appearances while sharing the same underlying structure.

## Asynchronous Programming
1. Use async and await: For tasks that can potentially block, such as loading resources or querying a database, use asynchronous programming to keep the game running smoothly.
2. Coroutines: Coroutines are useful for spreading work over several frames, executing tasks that need delays, or simplifying complex state machines without blocking game execution.

## Conditional compiler directives
1. All compiler directives should use SCREAMING_CAPS.
2. Add a comment for any `#else` or `#endif` indicating the relevant `#if` to clarify the conditional code - matching every conditional


## Namespace conventions
1. Use the prefix of the namespace with a company name to prevent conflicts.
2. Use PascalCase and separate namespace components with a period - i.e., `Company.Plugin`.
3. Prefer using plural namespace and don't use generic type names such as `Element`, `Node`, `Log`, and `Message`.
4. Do not use the same name as types in namespaces within a single application model.
5. Descriptive Names: Choose names that clearly and concisely convey the purpose of the variable. Avoid using names that require additional comments to explain, e.g., use elapsedTime instead of et
6. Action-Oriented Method Names: Use verbs or verb phrases to clearly indicate what the method does, making the purpose of the method immediately clear, e.g., DestroyObject, FindPlayer.


## Using statements
1. For Unity-based projects, list all **Unity** using statements at the top. **NOTE**: TMPro should be considered a Unity class, so typically starts the list.
2. List any Unity package or third-party plugins next.
3. List standard C# using statements next.
5. Order each of the above groups alphabetically.
6. Add a blank line between each using group (for clarity).
7. *EXCEPTION*: If specific functionality is required to override the above, order as necessary and add a comment explaining the reasoning behind the decision.


## Classes, structs, and interfaces
1. Use PascalCase; name classes and structs with nouns.
2. Name interfaces with adjective phrases or occasionally with nouns or noun phrases.
3. End the name of a derived class with the base class.


## Generic type parameters
1. Name generic type parameters with descriptive names unless a single-letter name is entirely self-explanatory.
2. Consider using  `T`  as the type parameter name for types with one single-letter type parameter - i.e., `public  int IComparer<T> { ... }`.


## Enums
1. Use a singular type name for an `enum` if values are bit fields. 
2. Use plural type for `Enum` with bit fields are `enum`. 
3. Do not use "Enum" "Flag" suffix in enum type names - **i.e.,** 
```sh
{
        EnumType1,
        EnumType2
}
```
4. Enums should use PascalCase.


## Methods  
1. Use methods names that are verbs or verb phrases - i.e., ` public int CompareTo(…);`.
2. Ensure method names are indicative of the function performed.
3. Ensure method names are updated if the underlying functionality changes.
4. Use concise language to accurately describe parameters (including `ref`, `out`, etc.).
5. Do not end parameter descriptions with a period (`.`).


## Properties  
1. Do name properties using a noun, noun phrase, or adjective.
2. Do name collection properties with a plural phrase describing the items in the collection instead of using a singular phrase followed by `List` or `Collection`.
3. Do name Boolean properties with an affirmative phrase - i.e., `“Is”`, `“Can”` or `“Has”`.


## Events
1. Do name events with a verb or a verb phrase.
2. Do use two parameters named sender and e in event handlers.
`public delegate void ClickedEventHandler(object sender, ClickedEventArgs e);`
3. Do name event argument classes with the `EventArgs` suffix.
4. Only call the events using Invoke().


## Delegates
1. Use the concise syntax to create instances of a `delegate` type.
```sh
// Define the type
public delegate void Del(string message);

// Define a method that has a matching signature
public static void DelMethod(string str)
{
    LogFile.Log($"DelMethod argument: {str}");
}
```
  
## Fields
1. Do use PascalCase in field names.
2. Do name fields using a noun, noun phrase, or adjective.
3. Do NOT use a prefix for field names.
4. **EXCEPTION FROM C# STANDARD** Use SCREAMING CAPS for constants

|Field Type      |Casing Type                    |Example                  |
|----------------|-------------------------------|-----------------------|
|Private Field   |LowerCamelCase              |_newPrivateField       |
|Public Field    |UpperCamelCase                |NewPublicField         |
|Protected Field |UpperCamelCase         |NewProtectedField     |
|Internal Field  |UpperCamelCase         |NewInternalField     |
|Property     |UpperCamelCase         |NewProperty            |
|Method         |UpperCamelCase         |NewMethod             |
|Class         |UpperCamelCase         |NewClass             |
|Interface     |IUpperCamelCase         |INewInterface             |
|Local Variable     |LowerCamelCase          |newLocalVariable       |
|Parameter     |LowerCamelCase         |newParameter            |
|Constants     |SCREAMING CAPS         |NEW_CONSTANT            |


## Arrays
1. Use the concise syntax when you initialize arrays on the declaration line.

// Preferred syntax. Note that you cannot use var here instead of string[].

`string[] vowels = { "a", "e", "i", "o", "u" };`


## Verbose debugging - scripting defines
1. Do wrap all debug logging with scripting defines
```sh
    #if VERBOSE_SYSTEM
        LogFile.Log($"{this.GetCaller(gameObject.name)} buttonIndex is 0");
    #endif  // VERBOSE_SYSTEM
```
2. Define scripting defines at the top of the file (in `#region Defines`).
3. Comment out scripting defines by default. Use the ScriptingDefines Unity ScriptableObject to set all active scripting defines.
4. Always include the scripting define in the `#endif`. See the example above.
5. Use interpolated strings to make variable usage more obvious. Never use `+`.
6. Always add a blank line _**before**_ and _**after**_ conditional code.
7. Indent the `#if` to the _**left**_ of the code - so that the code is aligned at the expected position (as if there was no conditional).
8. If the conditional code is more than one line, insert blank lines _**before**_ and _**after**_. This applies to the `#else` condition.


## Best practices for exceptions
1. Use `try`/`catch`/`finally` blocks to recover from errors or release resources.
2. Handle common conditions _without_ throwing exceptions.
3. Throw exceptions instead of returning an error code.
4. End exception class names with the word `Exception` - i.e., of `try-catch`
```sh
try 
{
  //  Block of code to try
}
catch (Exception e)
{
  //  Block of code to handle errors
}
```

## Implicitly-typed variables
1. Do NOT use implicitly-typed variables (**`var`**).


## Method summary  
1. Unless part of **SubCore**, do **NOT** include method summaries. **SubCore** is treated differently (as if it were some type of API).
```sh
/// <summary>
///
/// </summary>
```
**NOTE**: We are not generating documentation for individual modules, and rather than seeing inaccurate summaries, nothing is preferred - the code should be clear enough...


## Do's and don'ts
1. Do NOT use **underscores** in identifiers. **EXCEPTION**: **`private`** variables begin with an underscore.
```sh
// Correct
public DateTime ClientAppointment;
public TimeSpan TimeLeft;
public static Manager Instance;
 
// Avoid
public DateTime Client_Appointment;
public TimeSpan Time_Left;
private float line_length;

// Exception
private float _lineLength;
private static DateTime _registrationDate;
```

2. Do name source files according to their main classes. **EXCEPTION**: File names with partial classes reflect their source or purpose - i.e., `designer`, `generated`.
```sh 
// Located in Worker.cs
public partial class Worker
{
    //...
}
```

3. Do not explicitly specify a type of an **enum or values of enums** (except bit fields).
```sh
// Do not
public enum Direction : long
{
}
 
// Correct
public enum Direction
{
}
```

4. Do organize **namespaces** with a clearly defined structure.
```sh
// Examples
namespace Company.Product.Module.SubModule
namespace Product.Module.Component
```

5. Do vertically align **curly brackets**.
```sh
// Correct
class Program
{
    if (i < 0)
    {
    }
}
```

6. Do declare all member variables at the top of a class, with static variables at the very top.

    **EXCEPTION**: If `region`s are used to delineate functionality; the member variables should be defined at the top of the region.
```sh 
// Correct
public class Account
{
    public static string BankName;
 
    public string Number { get; set; }
    
 
    // Constructor
    public NewConstructor()
    {
        // ...
    }
}
```

7. Do use camelCase arguments for **constructors**.
```sh
public Car(Color bodyColor, int numOfDoors, int sizeOfWheels)
{
     BodyColor = bodyColor;
     NumOfDoors = numOfDoors;
     SizeOfWheels = sizeOfWheels;
}
```

8. Do surround all **calculations** with parenthesis to reinforce the intent - i.e., `_axisY -= (SpeedV * Input.GetAxis(Mouse_Y));`
9. Do surround ternary conditionals with parenthesis - i.e., `string usedText = (used ? "TRUE" : "FALSE");`
10. Do specify **floating-point numbers** as `n.nf` - i.e., `1.0f`, `2.1f`, to at least one (1) decimal place.
11. Do use **`protected`** or **`private`** specifiers to the class member if they will not be accessed from another class.
12. Do use **`protected`** specifiers for standard Unity methods (`Awake()`, `Start()`, `OnEnable()`, etc.)
15. Do remove unused functions or blocks of commented-out code.
16. Do NOT use **MAGIC NUMBERS**. Consider replacing the number with a named constant. Place those constants in a common file (i.e., `S.CS` or some variation thereof).
17. Avoid using the component name in variables of that type.
18. Do group related methods together.
20. MacOS users should ensure that `*.DS_Store` is present in the `.gitignore` file to remove temporary MacOS files before committing any files.
21. Do use modern language features to improve readability - expression-bodied methods, local functions, etc.
22. Do use verbose debug logs - they can help track issues faster than just staring at the code...


## Recommended tools to help improve overall code quality
1. Linters - i.e., StyleCop
2. VisualCodeGrepper
3. UnityCodeCoverage
4. IDE plugins - ReSharper or OmniSharp
5. UnityTestFramework
6. The following are recommended extensions for our preferred editor (Visual Studio Code):
    * C# for Visual Studio Code (powered by OmniSharp)
    * C# XML Documentation Comments
    * Code Spell Checker
    * Coding Tracker
    * Gremlins tracker for Visual Studio Code
    * markdownlint
    * Trailing Spaces
    * Visual Studio Intellisense

