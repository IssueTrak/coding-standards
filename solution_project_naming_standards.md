Solution and Project Naming Standards
===========================================

Date Created: 2015-06-12
Last Modified: 2016-06-21

## Summary

This document describes the conventions and best practices applicable to naming Issuetrak .NET solutions and projects.


* Solution folders should match physical folders on disk
* Project names should derive from the path of project, relative to the repository root, and starting with "Issuetrak"
* Folders, project names, and namespaces should contain only alphabetical and "dot" (.) characters
* If a folder contains only a project of the same name as the folder, then the folder is unnecessary, the project should be moved up one directory, and the folder should be discarded
* Add '.Tests' on to the end of a project's corresponding unit test library
    * Project = "Issuetrak.Common.Security"
    * Unit Test Library = "Issuetrak.Common.Security.Tests"
* Do not use items in the name that can be easily gauged by looking at it in Visual Studio
    * i.e. If the project is a class library, DO NOT use 'library' in the project name

## Best Practices

* Use folders to group a library project with its unit test project