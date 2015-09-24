# IssueTrak Software Development Fundamentals

Author: [Ken Taylor](mailto:ken.taylor@issuetrak.com?subject=IssueTrak%20Software%20Development%20Fundamentals)  
Date Created: 2015-09-24  
Last Updated: 2015-09-24  

The following four (4) practices are fundamental to success as professional software engineers and as such are central to our software development efforts at IssueTrak.

## 1) We write "Clean Code"

> "Clean code is simple and direct. Clean code reads like well-written prose. Clean code never obscures the designer's intent but rather is full of crisp abstractions and straightforward lines of control."
> -Grady Booch

Because we recognize that software can be expensive to maintain when it is not well written: _Software written for ANY development project at IssueTrak must be written using the [clean coding fundamentals][cleancode]._ Much of the principles outlined below can be found in [Robert C. Martin's][unclebob] (AKA Uncle Bob) [Clean Code: A Handbook of Agile Software Craftsmanship book][ccbook].

These fundamentals include (_but are not limited to_):

### Naming

Names of classes, variables, methods, functions, etc. should reveal the intention. For that reason (and others, we use [Tim Ottinger's Rules for Variable and Class Naming][ottingers].

### Functions

> "FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY."
> -Robert C. Martin

Functions should:

* Be small (3 lines is the goal - extract til you drop)
* Do one thing
* Avoid switch statements (they are typically a hint to use polymorphism)
* Use descriptive names
* Have few arguments
* Have no side effects (i.e. output arguments)
* Prefer Exceptions to Returning Error Codes

### Comments

> "Don't comment bad code -- rewrite it."
>  -Brian W. Kernighan and P.J. Plaugher

Largely, comments should be viewed as a failure to express yourself properly in the source code. The code should express its intent and not need comments to explain it. Comments tend to rot faster than the rest of the source code and can be a source of disinformation. Avoid them unless absolutely necessary. We use version control, so commented out code should be deleted with extreme prejudice.

There are a few _Good_ comments:

* Legal comments
* Informative Comments
* Explanation of Intent
* Clarification
* Warning of Consequences
* TODO Comments
* Amplification
* Documenting public APIs

The only truly good comment is the comment you found a way NOT TO WRITE.

### Formatting

> "When people look under the hood, we want them to be impressed with the neatness, consistency, and attention to detail that they perceive. We want them to be struck by the orderliness. We want their eyebrows to rise as they scroll through the modules. We want them to perceive that professionals have been at work."
> -Robert C. Martin (on Formatting)

The code should be neat and uniform. Code formatting is about communication!

#### Vertical Formatting

* Small files 200-500 lines should be considered desirable. Small files are usually easier to understand.
* The code should be written almost like a newspaper article, with the high-level synopsis at the top and all of the details increasingly as you move to the bottom.
* There should be 1 blank line between concepts (i.e. vertical openness between concepts)
* Concepts that are closely related should be kept together (i.e. one under the other) -- there should not be unrelated concepts separating them if at all possible.
    * Dependent functions should be vertically close.
* Variable declarations should be as close to their usage as possible.
* Instance variables should be declared at the top of the class.

#### Horizontal Formatting

* Lines should be be kept as short as possible.
* 100 -120 characters should be the upper limit for lines.
* Proper indentation should be used.

## 2) We adhere to coding standards

IssueTrak has defined coding standards for the languages we commonly use. Follow them.

* [C# coding standards](csharp_coding_standards.md)
* [HTML/CSS coding standards](html_css_coding_standards.md)
* [Javascript coding standards](javascript_coding_standards.md)
* [ASP coding standards](asp_coding_standards.md) 

If there are changes that you would like to recommend, do a [pull request][pullrequest].

## 3) We unit test our code

> "Code without tests is bad code. It doesn't matter how well written it is; it doesn't matter how pretty or  object-oriented or well- encapsulated it is. With tests, we can change the behavior of our code quickly and verifiably. Without them, we really don't know if our code is getting better or worse."
> -Michael C. Feathers (Working Effectively With Legacy Code) 

Because we recognize that code written without unit tests is already legacy code, we write unit tests for all of the code we can write unit tests for. 

We practice [TDD (Test Driven Development)][tdd] because this is the most efficient way to ensure our tests our being created. The benefits of this are:

* Easier/less debugging
* Loosely coupled code
* A comprehensive test suite

## 4) We conduct code reviews

We practice [peer code reviews][review] as a team to ensure we maintain a high quality of code and to spot potential design flaws. 

To do this, we:

* Recognize our source code is our design, so we keep it clean -- as in [clean code][cleancode].
* Give fair and helpful reviews of other developers code and we have our individual code reviewed by others.

### Guiding Principal

_"Can I read and quickly understand the source code"_ is the primary guiding principal in conducting a code review.    
If the answer is __NO__, the source code is __NOT__ fit for production.

### Checklist

We use the [code review checklist][checklist] to remind us of the areas we need to check.

---
[cleancode]: https://cleancoders.com/category/fundamentals
[unclebob]: https://en.wikipedia.org/wiki/Robert_Cecil_Martin
[ccbook]: http://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882
[ottingers]: ottingers-rules-for-naming.pdf
[pullrequest]: http://yangsu.github.io/pull-request-tutorial/
[tdd]: https://en.wikipedia.org/wiki/Test-driven_development
[review]: https://en.wikipedia.org/wiki/Code_review
[checklist]: code_review_checklist.md