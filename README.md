# Kotlin Style Guide (in progress)

Our overarching goals are __conciseness__, __readability__ and __simplicity__.

## Inspiration

This style-guide is somewhat of a mash-up between the existing Kotlin language style guides, and a tutorial-readability focused Swift style-guide. The language guidance is drawn from: 

- The [Android Kotlin style guide](https://android.github.io/kotlin-guides/style.html)
- The [Kotlin Coding Conventions](https://kotlinlang.org/docs/reference/coding-conventions.html) 
- The [Android contributors style guide](https://source.android.com/source/code-style.html)
- The [Google Java Style Guide](https://google-styleguide.googlecode.com/svn/trunk/javaguide.html).

## Android Studio Coding Style

It is possible to get Android Studio to adhere to these style guidelines, via a rather complex sequence of menus. To make it easier, we've provided a coding style that can be imported into Android Studio.

The file can be found [here](https://koenig-media.raywenderlich.com/uploads/2018/03/rwstyle.xml_.zip).

To install the file, open Android Studio Settings and go to **Editor > Code Style > Kotlin**, then click the gear menu and choose **Import Scheme...**.

From now on, projects you create _should_ follow the correct style guidelines.


## Table of Contents

- [Nomenclature](#nomenclature)
  + [Packages](#packages)
  + [Classes & Interfaces](#classes--interfaces)
  + [Methods](#methods)
  + [Fields](#fields)
  + [Variables & Parameters](#variables--parameters)
  + [Misc](#misc)
  + [Id's](#id's)
  + [Имена стилей](#имена-стилей)
- [Declarations](#declarations)
  + [Visibility Modifiers](#visibility-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Classes](#classes)
  + [Структура класса](#структура-класса)
  + [Data Type Objects](#data-type-objects)
- [Enum Classes](#enum-classes)
  - [Enum с конструктором](#enum-с-конструктором)
  - [Enum с методами](#enum-с-методами)
- [Spacing](#spacing)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Semicolons](#semicolons)
- [Getters & Setters](#getters--setters)
- [Brace Style](#brace-style)
- [When Statements](#when-statements)
- [Annotations](#annotations)
- [Types](#types)
  + [Type Inference](#type-inference)
  + [Constants vs. Variables](#constants-vs-variables)
  + [Companion Objects](#companion-objects)
  + [Optionals](#optionals)
- [XML Guidance](#xml-guidance)
- [Language](#language)
- [Copyright Statement](#copyright-statement)
- [Smiley Face](#smiley-face)
- [Credit](#credits)


## Nomenclature

On the whole, naming should follow Java standards, as Kotlin is a JVM-compatible language.

### Packages

Package names are similar to Java: all __lower-case__, multiple words concatenated together, without hypens or underscores:

__BAD__:

```kotlin
com.RayWenderlich.funky_widget
```

__GOOD__:

```kotlin
com.raywenderlich.funkywidget
```

### Classes & Interfaces

Written in __UpperCamelCase__. For example `RadialSlider`. 

### Methods

Written in __lowerCamelCase__. For example `setValue`.

### Fields

Generally, written in __lowerCamelCase__. Fields should **not** be named with Hungarian notation, as Hungarian notation is [erroneously thought](http://jakewharton.com/just-say-no-to-hungarian-notation/) to be recommended by Google.

Example field names:

```kotlin
class MyClass {
  var publicField: Int = 0
  val person = Person()
  private var privateField: Int?
}
```

Constant values in the companion object should be written in __uppercase__, with an underscore separating words:

```kotlin
companion object {
  const val THE_ANSWER = 42
}
```

### Variables & Parameters

Written in __lowerCamelCase__.

Single character values must be avoided, except for temporary looping variables.

### Misc

In code, acronyms should be treated as words. For example:

__BAD:__

```kotlin
XMLHTTPRequest
URL: String? 
findPostByID
```
__GOOD:__

```kotlin
XmlHttpRequest
url: String
findPostById
```

### Id's

Правило Where-What-Description. Например `fragment_authorization_text_view_password_hint`. Удобно для автокомплита

### Имена стилей

Порядок такой:

1. Название View, к которому применяется стиль

2. Место применения (Если стиль будет применяться во всём проекте, то это можно опустить)

3. Описание (Если требуется 2 почти одинаковых стиля, в которых различаются несколько параметров. Например, разный цвет текста или фона)

   ```xml
       <style name="InputField.Field" parent="android:Widget.EditText">
           <item name="android:textColor">@color/accent</item>
           <item name="android:textColorHint">@color/gray_BD</item>
           <item name="fontFamily">@font/sf_pro_bold</item>
           <item name="android:textSize">16sp</item>
           <item name="android:background">@android:color/transparent</item>
       </style>
   
       <style name="InputField.Field.Light" parent="android:Widget.EditText">
           <item name="android:textColor">@color/accent</item>
           <item name="android:textColorHint">@color/gray_BD</item>
           <item name="fontFamily">@font/sf_pro</item>
           <item name="android:textSize">16sp</item>
           <item name="android:background">@drawable/d_border</item>
       </style>
   ```

   ```xml
   	<style name="TextView.BottomSheetDialog.Header">
       	<item name="android:textColor">@android:color/white</item>
       	<item name="fontFamily">@font/sf_pro_bold</item>
       	<item name="android:textSize">16sp</item>
   	</style>
   ```

## Declarations

### Visibility Modifiers

Only include visibility modifiers if you need something other than the default of public.

**BAD:**

```kotlin
public val wideOpenProperty = 1
private val myOwnPrivateProperty = "private"
```

**GOOD:**

```kotlin
val wideOpenProperty = 1
private val myOwnPrivateProperty = "private"
```

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and member variables.

### Fields & Variables

Prefer single declaration per line.

__GOOD:__

```kotlin
username: String
twitterHandle: String
```

### Classes

Exactly one class per source file, although inner classes are encouraged where scoping appropriate.

### Структура класса

1) companion object
2) Поля: `abstract`, `override`, `public`, `internal`, `protected`, `private`
3) Блок инициализации: `init`, `конструкторы`
4) Абстрактные методы
5) Переопределенные методы родительского класса (желательно в том же порядке, в каком они следуют в родительском классе)
6) Реализации методов интерфейсов (желательно в том же порядке, в каком они следуют в описании класса, соблюдая при этом порядок описания этих методов в самом интерфейсе)
7) `public` методы
8) `internal` методы
9) `protected` методы
10) `private` методы
11) `inner` классы

### Data Type Objects

Prefer data classes for simple data holding objects.

__BAD:__

```kotlin
class Person(val name: String) {
  override fun toString() : String {
    return "Person(name=$name)"
  }
}
```

__GOOD:__

```kotlin
data class Person(val name: String)
```

## Enum Classes

Enum classes without methods may be formatted as follows:

```kotlin
private enum CompassDirection { 
    EAST, NORTH, WEST, SOUTH 
}
```

### Enum с конструктором

Если есть конструктор, то каждый элемент должен занимать свою строку

```kotlin
private enum Numbers(val num: Int) { 
    ONE(1), 
    TWO(2), 
    THREE(3), 
    FOUR(4) 
}
```

### Enum с методами

#### 	С конструктором

```kotlin
private enum Numbers(val num: Int) { 
    ONE(1), 
    TWO(2), 
    THREE(3), 
    FOUR(4);
    
    override fun toString(): String {
        return "${this.name} | ${this.num}"
    }
}
```

#### 	Без конструктора

```kotlin
private enum Numbers { 
    ONE, TWO, THREE, FOUR;
    
    override fun toString(): String {
        return this.name
    }
}
```



## Spacing

Spacing is especially important in code, as code needs to be easily readable. 

### Line Length

Lines should be no longer than 100 characters long.


### Vertical Spacing

There should be exactly one blank line between methods to aid in visual clarity and organization. Whitespace within methods should separate functionality, but having too many sections in a method often means you should refactor into several methods.

## Comments

When they are needed, use comments to explain **why** a particular piece of code does something. Comments must be kept up-to-date or deleted.

Avoid block comments inline with code, as the code should be as self-documenting as possible. *Exception: This does not apply to those comments used to generate documentation.*


## Semicolons

Semicolons ~~are dead to us~~ should be avoided wherever possible in Kotlin. 

__BAD__:

```kotlin
val horseGiftedByTrojans = true;
if (horseGiftedByTrojans) {
  bringHorseIntoWalledCity();
}
```

__GOOD__:

```kotlin
val horseGiftedByTrojans = true
if (horseGiftedByTrojans) {
  bringHorseIntoWalledCity()
}
```

## Getters & Setters

Unlike Java, direct access to fields in Kotlin is preferred. 

If custom getters and setters are required, they should be declared [following Kotlin conventions](https://kotlinlang.org/docs/reference/properties.html) rather than as separate methods.

## Brace Style

Only trailing closing-braces are awarded their own line. All others appear the same line as preceding code:

__BAD:__

```kotlin
class MyClass
{
  fun doSomething()
  {
    if (someTest)
    {
      // ...
    }
    else
    {
      // ...
    }
  }
}
```

__GOOD:__

```kotlin
class MyClass {
  fun doSomething() {
    if (someTest) {
      // ...
    } else {
      // ...
    }
  }
}
```

Conditional statements are always required to be enclosed with braces, irrespective of the number of lines required.

__BAD:__

```kotlin
if (someTest)
  doSomething()
if (someTest) doSomethingElse()
```

__GOOD:__

```kotlin
if (someTest) {
  doSomething()
}
if (someTest) { doSomethingElse() }
```

## When Statements

Unlike `switch` statements in Java, `when` statements do not fall through. Separate cases using commas if they should be handled the same way. Always include the else case.

__BAD:__

```kotlin
when (anInput) {
  1 -> doSomethingForCaseOneOrTwo()
  2 -> doSomethingForCaseOneOrTwo()
  3 -> doSomethingForCaseThree()
}
```

__GOOD:__

```kotlin
when (anInput) {
  1, 2 -> doSomethingForCaseOneOrTwo()
  3 -> doSomethingForCaseThree()
  else -> println("No case satisfied")
}
```


## Types 

Always use Kotlin's native types when available. Kotlin is JVM-compatible so **[TODO: more info]**

### Type Inference

Type inference should be preferred where possible to explicitly declared types. 

__BAD:__

```kotlin
val something: MyType = MyType()
val meaningOfLife: Int = 42
```

__GOOD:__

```kotlin
val something = MyType()
val meaningOfLife = 42
```

### Constants vs. Variables 

Constants are defined using the `val` keyword, and variables with the `var` keyword. Always use `val` instead of `var` if the value of the variable will not change.

*Tip*: A good technique is to define everything using `val` and only change it to `var` if the compiler complains!

### Companion Objects

** TODO: A bunch of stuff about companion objects **

### Nullable Types

Declare variables and function return types as nullable with `?` where a `null` value is acceptable.

Use implicitly unwrapped types declared with `!!` only for instance variables that you know will be initialized before use, such as subviews that will be set up in `onCreate` for an Activity or `onCreateView` for a Fragment.

When naming nullable variables and parameters, avoid naming them like `nullableString` or `maybeView` since their nullability is already in the type declaration.

When accessing a nullable value, use the safe call operator if the value is only accessed once or if there are many nullables in the chain:

```kotlin
editText?.setText("foo")
```



## XML Guidance

Since Android uses XML extensively in addition to Kotlin and Java, we have some rules specific to XML. These can be found in our [Java code standards](https://github.com/raywenderlich/java-style-guide#xml-guidance)


## Language

Use `en-US` English spelling. 🇺🇸

__BAD:__

```kotlin
val colourName = "red"
```

__GOOD:__

```kotlin
val colorName = "red"
```

## Copyright Statement

The following copyright statement should be included at the top of every source file:

```
/* 
 * Copyright (c) 2020 Razeware LLC
 * 
 * Permission is hereby granted, free of charge, to any person obtaining a copy
 * of this software and associated documentation files (the "Software"), to deal
 * in the Software without restriction, including without limitation the rights
 * to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 * copies of the Software, and to permit persons to whom the Software is
 * furnished to do so, subject to the following conditions:
 * 
 * The above copyright notice and this permission notice shall be included in
 * all copies or substantial portions of the Software.
 * 
 * Notwithstanding the foregoing, you may not use, copy, modify, merge, publish,
 * distribute, sublicense, create a derivative work, and/or sell copies of the
 * Software in any work that is designed, intended, or marketed for pedagogical or
 * instructional purposes related to programming, coding, application development,
 * or information technology.  Permission for such use, copying, modification,
 * merger, publication, distribution, sublicensing, creation of derivative works,
 * or sale is expressly withheld.
 * 
 * This project and source code may use libraries or frameworks that are
 * released under various Open-Source licenses. Use of those libraries and
 * frameworks are governed by their own individual licenses.
 * 
 * THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 * IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 * FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 * AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 * LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 * OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
 * THE SOFTWARE.
 */
```

## Smiley Face

Smiley faces are a very prominent style feature of the raywenderlich.com site! It is very important to have the correct smile signifying the immense amount of happiness and excitement for the coding topic. The closing square bracket ] is used because it represents the largest smile able to be captured using ASCII art. A closing parenthesis ) creates a half-hearted smile, and thus is not preferred.

Bad:

    :)

Good:

    :]

## Credits

This style guide is a collaborative effort from the most stylish
raywenderlich.com team members:

- [Darryl Bayliss](https://github.com/DarrylBayliss)
- [Tom Blankenship](https://github.com/tgblank)
- [Sam Davies](https://github.com/sammyd)
- [Mic Pringle](https://github.com/micpringle)
- [Ellen Shapiro](https://github.com/designatednerd)
- [Ray Wenderlich](https://github.com/rwenderlich)
- [Joe Howard](https://github.com/orionthwake)
