Unit Test Guidelines and Best Practices
=================================

Date Created: 2015-05-04  
Last Modified: 2015-05-04    

## Summary

This document describes the conventions and best practices applicable to IssueTrak project repositories. They are roughly based on [Roy Osherove's naming standards for unit tests][namingstandards].

### Table of Contents

- [Naming Unit Test Projects](#naming-unit-test-projects)
- [Naming Unit Test Classes](#naming-unit-test-classes)
- [Naming Unit Test Methods Tests](#naming-unit-test-methods)
- [Naming Integration Test Projects](#naming-integration-test-projects)
- [Best Practices](#best-practices)

## Naming Unit Test Projects

Unit test projects typically map one-to-one with a class library project. Unit test libraries are also class libraries in C#. The naming convention is to just use the same name as the class library with `.Tests` tacked on to the end.

Example:

If your class library is:
`IssueTrak.Domain.Common`

The unit test library that tests it will be:
`IssueTrak.Domain.Common.Tests`


## Naming Unit Test Classes

Naming the test classes in your project is relatively straight forward: 

If you have a class called `FooBar` the corresponding class in the unit test project will be `FooBarTest`

## Naming Unit Test Methods Tests

(NOTE: This is verbatim what you will find in [Roy Osherove's blog post][namingstandards])

The basic naming of a test comprises of three main parts:

    [UnitOfWork_StateUnderTest_ExpectedBehavior]

A unit of work is a use case in the system that startes with a public method and ends up with one of three types of results: a return value/exception, a state change to the system which changes its behavior, or a call to a third party (when we use mocks). so a unit of work can be a small as a method, or as large as a class, or even multiple classes. as long is it all runs in memory, and is fully under our control.

Examples:

    Public void Sum_NegativeNumberAs1stParam_ExceptionThrown()
    
    Public void Sum_NegativeNumberAs2ndParam_ExceptionThrown ()
    
    Public void Sum_simpleValues_Calculated ()

### Reasons:

**Test name should express a specific requirement**

Your unit test name should express a specific requirement. This requirement should be somehow derived from either a business requirement or a technical requirement. In any case, that requirement has been broken down into small enough pieces, each of which represents a test case. If your test is not representing a requirement, why are you writing it? Why is that code even there?

Also, developers who are on a role are happy to give meaningless or numbered names to their test just so they can continue on with what they are doing. This leads down a narrow slope where quickly no one has the time or energy to fix the names of the tests. Also, most developers don t bother too much with writing good assert messages in their tests. A good assert message (which shows up if the test fails) is jey to understanding what went wrong. Assuming writing good assert messages is one of the key places where most unit test developers fall short, the only thing left to save us then is the name of the test. If both the name of the test and the error messages in it are not expressive enough, the poor maintenance developer (often the same one who developed the tests) is left to wonder what was this joker thinking? looking at a year old code base with unit tests.

**Test name should include the expected input or state and the expected result for that input or state**

To express the specific requirement clearly you should think about two things you need to express: the input values/current state during which the test takes place, and the expected result from that state.

#### Example:

Given this method :

    Public int Sum(params int[] values)

You have a requirement that numbers larger than 1000 that are passed in should not be considered for calculation (that is a number bigger than 1000 is equal to zero).

**What about this name: Sum_NumberBiggerThan1000**

That is only half way there. As a reader of the test I can only assume that some input in your test is bigger than 1000, but I do not understand what the requirement being tested is.

**How about this name: Sum_NumberIsIgnored**

Still not good enough. While it does tell me the expected result, it does not tell me under which circumstances it needs to be ignored. I would have to go into the test code and read through it to find out what the expected input is.

**How about this name: Sum_NumberIgnoredIfBiggerThan1000**

That's much better. I can tell just by looking at the test name what It means if the test fails. I don t need to look at the code, and I can tell exactly what requirement this test tries to solve.

**Test name should be presented as a statement or fact of life that expresses workflows and outputs**

Unit tests are just as much about documentation as they are about testing functionality. You should always assume that someone else is going to read your tests in a year, and that they should not have a hard time understanding your intent.

Test names which are written as short declarative statements are much more expressive that names which are machine readable that is they only make sense if you have an understanding of a hidden code language to dissect their meaning.

People might first complain that the name of the test method appears way too long for them, but in the end it s more about readability. Longer test names do not imply longer or less optimized code, and even if they did, we are not looking to optimize test code performance. If anything, test code should always be optimized for readability.

Here's an example of a bad and good test name:

    Public void SumNegativeNumber2()

And here's a *better* way to express your intent:

    Public void Sum_ExceptionThrownOnNegativeNumberAs2ndParam ()

Test Name should only begin with Test if it is required by the testing framework or if it eases development and maintenance of the unit tests in some way.

Since most tests today reside in a specific class or module that is logically defined as a test container (fixture), there are only a handful of reasons why you would want to prefix you test methods with the word Test :

- Your unit testing framework requires this
- You have coding standards in place and they include this
- You want to make it easier to navigate to the methods using Intellisense or some other search mechanism.

Test name should include name of tested method or class

You usually have at least a number of tests for each method you are testing, and you are usually testing a number of methods in one test fixture (since you usually have a test fixture per class tested). This leads to the requirement that your test should also reflect the name of the method begin tested, not only the requirements from it.

For example:

[MethodName_StateUnderTest_ExpectedBehavior]

    Public void Sum_NegativeNumberAs1stParam_ExceptionThrown()

    Public void Sum_NegativeNumberAs2ndParam_ExceptionThrown ()

    Public void Sum_simpleValues_Calculated ()

    Public void Parse_OnEmptyString_ExceptionThrown()

    Public void Parse_SingleToken_ReturnsEqualToeknValue ()

**Naming Variables in a test:**

Variable names should express the expected input and state

It's easy to name variables going into a method with generic names, but with unit tests you have to be twice as careful to name them as what they represent, i.e. BAD_DATA or EMPTY_ARRAY or NON_INITIALIZED_PERSON

You do not need to name them with a CONST casing , but the name does have to represent the intent of the test author.

A good way to check if your names are good enough is to look at the ASSERT at the end of the test method. If the ASSERT line is expressing what your requirement is, or comes close, you re probably there.

For example:

    Assert.AreEqual(-1, val)
Vs.

    Assert.AreEqual(BAD_INITIALIZATION_CODE, ReturnCode, Method shold have returned a bad initialization code )

## Naming Integration Test Projects

If you are creating an integration test project, make sure it is named as such. **DO NOT** use "Test" in the naming.

Example:

If your class library is:
    
    IssueTrak.Domain.Common

The integration test library that tests it will be:
    
    IssueTrak.Domain.Common.Integration


## Best Practices

- Unit tests should be **FAST**
- Code tested by unit tests should be loosely coupled
- Unit tests are **NOT** integration tests

### A good unit test is:

- Able to be fully automated
- Has full control over all the pieces running (Use mocks or stubs to achieve this isolation when needed)
- Can be run in any order  if part of many other tests
- Runs in memory (no DB or File access, for example)
- Consistently returns the same result (You always run the same test, so no random numbers, for example. save those for integration or range tests)
- Runs fast
- Tests a single logical concept in the system
- Readable
- Maintainable
- Trustworthy (when you see its result, you don’t need to debug the code just to be sure

## Tools

### Mocking
[Moq][moq] (To install nuget package type `Install-Package moq` in Package Management Console)

### Misc
[FluentAssertions][fluentassertions] (To install nuget package type `Install-Package fluentassertions` in Package Management Console)

## Terminology & Definitions

|Term         						|Definition     													|
|-----------------------------------|-------------------------------------------------------------------|
|Unit test       						| A unit of work is a single logical functional use case in the system that can be invoked by some public interface (in most cases). A unit of work can span a single method, a whole class or multiple classes working together to achieve one single logical purpose that can be verified.|
|Integration test               	| An integration test is done to demonstrate that different pieces of the system work together. Integration tests cover whole applications, and they require much more effort to put together. They usually require resources like database instances and hardware to be allocated for them. The integration tests do a more convincing job of demonstrating the system works (especially to non-programmers) than a set of unit tests can, at least to the extent the integration test environment resembles production.|
| Mocking | Mocking is creating objects that simulate the behavior of real objects. |




[namingstandards]: http://osherove.com/blog/2005/4/3/naming-standards-for-unit-tests.html
[moq]: https://github.com/Moq/moq4
[fluentassertions]: https://github.com/dennisdoomen/fluentassertions
