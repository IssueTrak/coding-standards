JavaScript Coding Standards
===========================

Date Created: 2014-08-15  
Last Modified: 2014-08-15  

## Standards

The current standards derive from Douglas Crockford's [Code Conventions for the JavaScript Programming Language](http://javascript.crockford.com/code.html)

## Table of Contents

- [Comments](#comments)
- [Variable Declarations](#variable-declarations)
- [Function Declarations](#function-declarations)
- [Names](#names)
- [Statements](#statements)
- [Whitespace](#whitespace)
- [Bonus Suggestions](#bonus-suggestions)


### Comments

Be generous with comments. It is useful to leave information that will be read at a later time by people (possibly yourself) who will need to understand what you have done. The comments should be well-written and clear, just like the code they are annotating. An occasional nugget of humor might be appreciated. Frustrations and resentments will not.

It is important that comments be kept up-to-date. Erroneous comments can make programs even harder to read and understand.

Make comments meaningful. Focus on what is not immediately visible. Don't waste the reader's time with stuff like

```js
i = 0; // Set i to zero.
```

Generally use line comments. Save block comments for formal documentation.;

### Variable Declarations

All variables should be declared before used. JavaScript does not require this, but doing so makes the program easier to read and makes it easier to detect undeclared variables that may become implied globals. Implied global variables should never be used. Use of global variables should be minimized.

The var statement should be the first statement in the function body.

It is preferred that each variable be given its own line and comment. They should be listed in alphabetical order if possible.

```js
var currentEntry, // currently selected table entry
    level,        // indentation level
    size;         // size of table
```

JavaScript does not have block scope, so defining variables in blocks can confuse programmers who are experienced with other C family languages. Define all variables at the top of the function.

### Function Declarations

All functions should be declared before they are used. Inner functions should follow the var statement. This helps make it clear what variables are included in its scope.

There should be no space between the name of a function and the ( (left parenthesis) of its parameter list. There should be one space between the ) (right parenthesis) and the { (left curly brace) that begins the statement body. The body itself is indented four spaces. The } (right curly brace) is aligned with the line containing the beginning of the declaration of the function.

```js
function outer(c, d) {
    var e = c * d;

    function inner(a, b) {
        return (e * a) + b;
    }

    return inner(0, 1);
}
```

This convention works well with JavaScript because in JavaScript, functions and object literals can be placed anywhere that an expression is allowed. It provides the best readability with inline functions and complex structures.

```js
    function getElementsByClassName(className) {
        var results = [];
        walkTheDOM(document.body, function (node) {
            var array,                // array of class names
                ncn = node.className; // the node's classname

// If the node has a class name, then split it into a list of simple names.
// If any of them match the requested name, then append the node to the list of results.

            if (ncn && ncn.split(' ').indexOf(className) >= 0) {
			    results.push(node);
            }
        });
        return results;
    }
```
If a function literal is anonymous, there should be one space between the word function and the ( (left parenthesis). If the space is omited, then it can appear that the function's name is function, which is an incorrect reading.

```js
div.onclick = function (e) {
    return false;
};

that = {
    method: function () {
        return this.datum;
    },
    datum: 0
};
```

Use of global functions should be minimized.

When a function is to be invoked immediately, the entire invocation expression should be wrapped in parens so that it is clear that the value being produced is the result of the function and not the function itself.

```js
var collection = (function () {
    var keys = [], values = [];

    return {
        get: function (key) {
            var at = keys.indexOf(key);
            if (at >= 0) {
                return values[at];
            }
        },
        set: function (key, value) {
            var at = keys.indexOf(key);
            if (at < 0) {
                at = keys.length;
            }
            keys[at] = key;
            values[at] = value;
        },
        remove: function (key) {
            var at = keys.indexOf(key);
            if (at >= 0) {
                keys.splice(at, 1);
                values.splice(at, 1);
            }
        }
    };
}());
```

### Names

Names should be formed from the 26 upper and lower case letters (`A .. Z, a .. z`), the 10 digits (`0 .. 9`), and _ (underbar). Avoid use of international characters because they may not read well or be understood everywhere. Do not use $ (dollar sign) or \ (backslash) in names.

Do not use _ (underbar) as the first or last character of a name. It is sometimes intended to indicate privacy, but it does not actually provide privacy. If privacy is important, use the forms that provide private members. Avoid conventions that demonstrate a lack of competence.

Most variables and functions should start with a lower case letter.

Constructor functions that must be used with the new prefix should start with a capital letter. JavaScript issues neither a compile-time warning nor a run-time warning if a required new is omitted. Bad things can happen if new is not used, so the capitalization convention is the only defense we have.

Global variables should be in all caps. (JavaScript does not have macros or constants, so there isn't much point in using all caps to signify features that JavaScript doesn't have.)

### Statements

#### Simple Statements

Each line should contain at most one statement. Put a ; (semicolon) at the end of every simple statement. Note that an assignment statement that is assigning a function literal or object literal is still an assignment statement and must end with a semicolon.

JavaScript allows any expression to be used as a statement. This can mask some errors, particularly in the presence of semicolon insertion. The only expressions that should be used as statements are assignments and invocations.

#### Compound Statements

Compound statements are statements that contain lists of statements enclosed in { } (curly braces).

* The enclosed statements should be indented four more spaces.
* The { (left curly brace) should be at the end of the line that begins the compound statement.
* The } (right curly brace) should begin a line and be indented to align with the beginning of the line containing the matching { (left curly brace).
* Braces should be used around all statements, even single statements, when they are part of a control structure, such as an if or for statement. This makes it easier to add statements without accidentally introducing bugs.

#### Labels

Statement labels are optional. Only these statements should be labeled: `while, do, for, switch`.

##### return Statement

A return statement with a value should not use ( ) (parentheses) around the value. The return value expression must start on the same line as the return keyword in order to avoid semicolon insertion.

##### if Statement

The if class of statements should have the following form:

```js
    if (condition) {
        statements
    }
    
    if (condition) {
        statements
    } else {
        statements
    }
    
    if (condition) {
        statements
    } else if (condition) {
        statements
    } else {
        statements
    }
```

##### for Statement

A for class of statements should have the following form:

```js
for (initialization; condition; update) {
    statements
}

for (variable in object) {
    if (filter) {
        statements
    } 
}
```

The first form should be used with arrays and with loops of a predeterminable number of iterations.

The second form should be used with objects. Be aware that members that are added to the prototype of the object will be included in the enumeration. It is wise to program defensively by using the hasOwnProperty method to distinguish the true members of the object:

```js
for (variable in object) {
    if (object.hasOwnProperty(variable)) {
        statements
    } 
}
```

##### while Statement

A while statement should have the following form:

```js
while (condition) {
    statements
}
```

##### do Statement

A do statement should have the following form:

```js
do {
    statements
} while (condition);

```

Unlike the other compound statements, the do statement always ends with a ; (semicolon).

##### switch Statement

A switch statement should have the following form:

```js
switch (expression) {
case expression:
    statements
    break;

default:
    statements
}
```

Cases are not indented further than the containing "switch" line. This prevents over-indention for case-contained statements.

Each group of statements (except the default) should end with break, return, or throw. Do not fall through. After each break, return, or throw, there should be a blank line.

##### try Statement

The try class of statements should have the following form:

```js
try {
    statements
} catch (variable) {
    statements
}

try {
    statements
} catch (variable) {
    statements
} finally {
    statements
}
```

##### continue Statement

Avoid use of the continue statement. It tends to obscure the control flow of the function.

##### with Statement

The with statement should not be used.

### Whitespace

Blank lines improve readability by setting off sections of code that are logically related.

Blank spaces should be used in the following circumstances:

* A keyword followed by ( (left parenthesis) should be separated by a space.
```js
    while (true) {
```
* A blank space should not be used between a function value and its ( (left parenthesis). This helps to distinguish between keywords and function invocations.
* All binary operators except . (period) and ( (left parenthesis) and [ (left bracket) should be separated from their operands by a space.
* No space should separate a unary operator and its operand except when the operator is a word such as typeof.
* Each ; (semicolon) in the control part of a for statement should be followed with a space.
* Whitespace should follow every , (comma).

### Bonus Suggestions

#### {} and []

Use {} instead of new Object(). Use [] instead of new Array().

Use arrays when the member names would be sequential integers. Use objects when the member names are arbitrary strings or names.

#### , (comma) Operator

Avoid the use of the comma operator. (This does not apply to the comma separator, which is used in object literals, array literals, var statements, and parameter lists.)

#### Block Scope

In JavaScript blocks do not have scope. Only functions have scope. Do not use blocks except as required by the compound statements.

#### Assignment Expressions

Avoid doing assignments in the condition part of if and while statements.

Is

```js
    if (a = b) {
```
a correct statement? Or was

```js
    if (a == b) {
```
intended? Avoid constructs that cannot easily be determined to be correct.

#### === and !== Operators.

Use the === and !== operators. The == and != operators do type coercion and should not be used.

#### Confusing Pluses and Minuses

Be careful to not follow a + with + or ++. This pattern can be confusing. Insert parens between them to make your intention clear.

    total = subtotal + +myInput.value;
is better written as

    total = subtotal + (+myInput.value);
so that the + + is not misread as ++.

#### eval is Evil

The `eval` function is the most misused feature of JavaScript. Avoid it.

`eval` has aliases. Do not use the `Function` constructor. Do not pass strings to `setTimeout` or `setInterval`.
