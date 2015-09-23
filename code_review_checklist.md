# Code Review Checklist

Author: [Ken Taylor](mailto:ken.taylor@issuetrak.com?subject=SUBJECT)  
Date Created: 2015-09-23  
Last Updated: 2015-09-23  

This checklist is loosely based on [FogCreek's code review checklist][fogcreek].

## General

* Does the code work? Does it perform its intended function, the logic is correct etc.
* Is all the code easily understood?
* Does it conform to our agreed upon [code standards][standards]?
* Is there any redundant or duplicate code?
* Is the code as modular as possible?
* Can any global variables be replaced?
* Is there any commented out code?
* Do loops have a set length and correct termination conditions?
* Can any of the code be replaced with library functions?
* Can any logging or debugging code be removed?

## Security

* Are all data inputs checked (for the correct type, length, format, and range) and encoded?
* Where third-party utilities are used, are returning errors being caught?
* Are output values checked and encoded?
* Are invalid parameter values handled?

## Documentation

* Is the code self documenting? (no comments in the code)

## Testing

* Is the code testable? i.e. doesn't add too many or hide dependencies, unable to initialize objects, test frameworks can use methods etc.
* Do tests exist and are they comprehensive? i.e. has at least your agreed on code coverage.
* Do unit tests actually test that the code is performing the intended functionality?
* Are arrays checked for ‘out-of-bound’ errors?
* Could any test code be replaced with the use of an existing API?

---
[fogcreek]: http://blog.fogcreek.com/increase-defect-detection-with-our-code-review-checklist-example/
[standards]: https://github.com/IssueTrak/coding-standards/blob/master/csharp_coding_standards.md