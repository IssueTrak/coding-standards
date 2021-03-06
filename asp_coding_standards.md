ASP Coding Standards
====================

Date Created: 2014-08-15  
Last Modified: 2014-08-15  

## Standards

### Comments

Block comments should be placed directly above the Subroutine or Function it is referencing:

```vb
'===============================================================================
' This function validates the user. 
' If not valid, jump to appropriate page, otherwise just return.
'===============================================================================
Private Sub Setup_CheckToken()
```

### Header

Files should begin with the standard header and documentation (Use `Admin_ClassAdd.asp` for reference):

```vb
<%
Option Explicit
%>
<!-- #include file="Setup_Inc.asp" -->
<!-- #include file="Security_Inc.asp" -->
<%
Call InitiateSession()

'*******************************************************************************
'  Workfile: Admin_ClassAdd.asp
'  Abstract: 
' Reference: Core
'*******************************************************************************
%>
```

### Keyword Case

The VB Keywords (Dim, Private, Function, etc.) should be Capitalized:

```vb
Dim someVariable

Private Function SomeFunctionName(someParameter)
	' Do something here...
End Function

Public Sub SomeSubroutineName(someParameter)
	` Do something
End Sub

```

### Variable Declaration ("Dim")

Each variable declaration should occur on a separate line. Variables may be initialized on the same line as their declaration.


```vb
' incorrect
Dim someVariable, someOtherVariable

' correct
Dim someVariable
Dim someOtherVariable

' also correct
Dim initializedVariable: initializedVariable = 0
```

## Best Practices

1. **Option Explicit** should be at the top of each ASP file to force explicit declaration of variables in the file:

```vb
<%
Option Explicit
%>
``` 