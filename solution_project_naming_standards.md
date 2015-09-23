Solution and Project Naming Standards
===========================================

Date Created: 2015-06-12  
Last Modified: 2015-09-23

## Summary

This document describes the conventions and best practices applicable to naming IssueTrak .NET solutions and projects.

### Table of Contents

- [Solutions](#solutions)
- [Projects](#projects)
- [Best Practices](#best-practices)

## Solutions

TBD

## Projects

Use the following guidelines when creating new .NET projects (or renaming old)

* Only use a dot to separate multiple words. (i.e. `IssueTrak.Common.Security`)
* Add 'Tests' on to the end of a project's corresponding unit test library
    * Project = `IssueTrak.Common.Security`
    * Unit Test Library = `IssueTrak.Common.Security.Tests`
* Do not use items in the name that can be easily gauged by looking at it in Visual Studio
    * i.e. If the project is a class library, DO NOT use 'library' in the project name


## Best Practices

* Use folders to group a library project with it's unit test project