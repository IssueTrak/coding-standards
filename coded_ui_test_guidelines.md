Coded UI Test Guidelines and Best Practices
===========================================

Date Created: 2015-05-27
Last Modified: 2015-05-27

## Summary

This document describes the conventions and best practices applicable to IssueTrak's Coded UI test project.

### Table of Contents

- [Page Classes](#page-classes)
- [Test Classes](#test-classes)
- [Test Setup and Tear Down](#test-setup-and-tear-down)
- [Page Element Properties](#page-element-properties)
- [Best Practices](#best-practices)

## Page Classes
- Should be located under the PageObjects folder and categorized in a sub-folder.  For example, the UserAddPage.cs file should be located in \PageObjects\Users\ along with UserEditPage.cs, UserListAllPage.cs, etc.
- Should be named similar to the menu option that leads to the page (e.g. UserListAllPage.cs) or to the function of the page (PopupTaskEditPage.cs).  They do not have to be named the same as the .asp file for the page (pages can, and will, be renamed; especially as we move to .NET).
- Name should end with "```Page```" (e.g. UserListAllPage).
- Should be structured with the following #regions:
    - #region Private Fields
    - #region Constructors
    - #region Page Element Properties
    - #region Validators
    - #region Actions
- Should implement get-only (no setter) properties (in the Page Element Properties region) for elements on the page.
- Should implement action methods (in the Actions region) for all needed interactions on the page (e.g FillDescription, ClickTopSaveButton, etc.)
    - Action methods should return an instance of the page class representing the page the action will end up on.  Returning ```this``` (the same page object the action is being called on) if the action doesn't leave the current page is perfectly acceptable.  This allows for a fluent style of coding by chaining method calls (e.g. ```submitPage.FillSubject("...").FillDescription("...").ClickSubmitButton()```).
- Should throw exceptions if errors are detected (```Assert``` should only be used in test classes).

### Non-Popup Page Classes
- Should inherit from the ```PageObject``` base class.
- Should implement the ```IPageObject``` interface.

### Popup Page Classes
- Name should start with "```Popup```" (e.g. PopupTaskManagerPage)
- Should be a generic class taking one type parameter named ```TParentPage```.
- Constructors should receive the popup's parent page object and pass it to the base class.
- Should inherit from ```PopupPageObject<TParentPage>``` generic base class.
- Should implement the ```IPageObject``` interface.

## Test Classes

- Should generally map one-to-one with a page.  For example, ```SubmitPageTest.cs``` will contain all the tests for the Issue Submit page.
- Name should start with the Page Class' name and end with "Test" (e.g. PopupTaskEditPageTest)
- Should not make any assumptions about the configuration of the site (e.g. Tasks enabled) or existence of data (e.g. IssueTrak Organization exists).
- Should use the Page objects to setup any needed configuration or data before the test and tear down when finished with the test.
- Should use try/catch around any setup and/or tear down code
- Should use ```Assert``` statements to enforce test results.
- Should be tagged with one or more ```TestCategory``` attributes to specify whether the test is for Regression, Build Acceptance, Release Acceptance, etc.
    - Pass the TestCategory attribute one of the Category constants (e.g. ```[TestCategory(Category.Regression)]```).  Do not pass "magic" strings (e.g. ```[TestCategory("Regrssion"]```).

## Test Setup and Tear Down
In a perfect world the entire back end would be mocked and the test would provide mock data (mock issues, users, configuration, etc.).  Since this is not feasible with the classic ASP product, we must have real data and configuration setup for our tests.  For now this should be done by using Coded UI to interact with the product and create the configuration and data a test needs and clean that data up.

For example, when a test starts it might (for setup) log in as Admin, create a user with specific permissions, enable tasks, and submit an Issue assigned to that user with a task.  Then it would perform the actual test by logging in as that user, navigating the Issue created during setup and performing some actions/asserts.  Last, (for tear down) it would log in as Admin and delete the user and issue it created.

- Tests can assume that the system default data exists and can use (but not modify) existing data (the Admin user, the IssueTrak organization, etc.)
- Tests should not modify any system default data.  If modifying the data is required then setup should create new data for the test to use and tear down should delete that data.
- Setup should create any data it needs (users, organizations, issues, etc.) using Environment.MachineName as the base for a unique string (for User ID, Organization name, etc).
- Tear down should delete any data created during setup and/or test.
- Tear down should leave any configuration changes made during setup and/or test. The reason for this is because each test sets up its own configuration and so *shouldn't* be affected by configuration changes of another test.  Also having to check and remember the state of configuration before setup/test in order to set configuration back during tear down adds possibly unnecessary effort to creating the tests.

## Page Element Properties
-- To Do

## Best Practices
-- To Do
