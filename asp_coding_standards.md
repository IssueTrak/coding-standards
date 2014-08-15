ASP Coding Standards
====================

## Standards

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


## Best Practices

1. **Option Explicit** should be at the top of each ASP file to force explicit declaration of variables in the file:

```vb
<%
Option Explicit
%>
``` 