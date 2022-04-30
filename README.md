# Coding Style Guide (C#)

### CONTENT

1.	Naming.
2.	Structure.
3.	Other.
4.	Helpers and extension methods.
5.	Tests.

### NAMING

1.	Constants must be uppercase.
2.	Fields start with `_` (underscore) prefix.
3.	Local variables start with lowercase.
4.	Parameters start with lowercase.
5.	Interface start with `I` prefix.
6.	Type parameters start with `T` prefix.
7.	Methods start with uppercase.
8.	Events start with uppercase.
9.	Enum members start with uppercase.
10.	All other members start with uppercase.

### STRUCTURE

1.	Constants.
2.	Static fields.
3.	Private fields. 
4.	Protected fields.
5.	Public properties.
6.	Constructor (if present).
7.	Public methods.
8.	Protected methods.
9.	Private methods.

### OTHER

1.	All constants except in tests should be class members rather than local.
2.	No whitespaces at the end of the lines.
3.	No empty lines after classes or namespaces.
4.	All starting brackets `{` should be on new line. With the exception of empty classes or methods.
5.	One class or enum means we should have one `.cs` file.
6.	Comments can be added only for exceptional cases. Use meaningful names instead of comments.
7.	Use `var` for declaring variables.
8.	Use `==` to compare objects instead of `Equals` if there is no reason to use `Equals`.
9.	Use `.Any()` instead of `.Count > 0` for Lists.
10.	Do not set value for variable on declaration if it is the same as default (like `false` for `bool` or `0` for integer).
11.	Delete unused assemblies.
12.	Avoid using `#region`.
13.	Delete redundancies code - warnings:
-	Qualifier is redundant,
-	Empty object or collection initializer list is redundant.
14.	Delete redundancies code - hint:
-	Empty argument list is redundant,
-	Parentheses are redundant if attribute has no arguments,
-	Redundant `else` keyword,
-	Redundant lambda signature parentheses.

### HELPERS AND EXTENSION METHODS

1.	All extension methods should be implemented in files named `XxxxExtensions` (where `Xxxx` is a class name which extension is applied to) in dedicated folder (`Extensions`).
2.	Do NOT add extension methods in Helpers classes.
3.	All helpers’ classes should be implemented in files named `XxxxHelpers` in dedicated folder (Helpers).
4.	Helpers class should implement its own interface.

### TESTS

1. Use FluentAssertions library.
2.	Tests with condition should be named as follows 

`GivenPreconditions_WhenBehaviourName_ThenExpectedBehavior` 

Example: 

`GivenAccountExpired_WhenGetPrepaidAccountDetails_ThenCorrectResultReturned`

3.	Tests without condition should be named as follows

`WhenBehaviourName_ThenExpectedBehavior` 

Example: 

`WhenAnalyticsViewNameAssigned_ThenContainsCorrectValue`

4.	API tests must be located under separate folder in Test’s project.
5.	All tests must be located in Test’s project.
6.	Every test class should be located in similar folder path as tested class.
7.	Test body should be divided into 3 sections by comments:
-	`// Arrange` 
-	`// Act` 
-	`// Assert`

8.	Each section should be separated by empty line.
9.	If all arranges are inside `// Act` section - `// Arrange` comment still should be written before `// Act` even if its empty (in that case, no empty line between is needed).
10.	If assert and act are the same piece of code and cannot be divided, then section should be named as follows:

```csharp
// Act
// Assert
result.Should().Be(“Example”);
```

11.	Test structure:

```csharp
[Fact]
public void ValidateAddArticle_WhenAllFieldsAreCorrect_ShouldFinishSuccessfully() 
{
    // Arrange
    var command = new AddArticleCommand 
    { 
        title = DataProvider.GetRandomString(),
        description = DataProvider.GetRandomString(),
        textToUpload = DataProvider.GetRandomString(),
        imageToUpload = DataProvider.GetRandomString()
    };

    // Act
    var validator = new AddArticleCommandValidator();
    var result = validator.Validate(command);

    // Assert
    result.Errors.Should().BeEmpty();
}
```
