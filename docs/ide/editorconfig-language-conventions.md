---
title: .NET language conventions for EditorConfig
ms.date: 06/17/2019
ms.topic: reference
dev_langs:
  - "CSharp"
  - "VB"
helpviewer_keywords:
  - "language code style rules [EditorConfig]"
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "dotnet"
  - "dotnetcore"
---
# Language conventions

Language conventions for EditorConfig in Visual Studio fall into two categories:

- [.NET code style settings](#net-code-style-settings)

- [C# code style settings](#c-code-style-settings)

> [!TIP]
> To see the code examples in your preferred programming language, choose it using the language picker at the top-right corner of the browser window.

## Rule format

Rules for language conventions have the following general format:

`option_name = value:severity`

For each language convention, you specify a value that defines if or when to prefer the style. Many rules accept a value of `true` (prefer this style) or `false` (do not prefer this style); others accept values such as `when_on_single_line` or `never`. The second part of the rule specifies the **severity**.

### Severity

A language convention severity specifies the level at which to enforce that style. The following table lists the possible severity values and their effects:

Severity | Effect
:------- | ------
`none` | Do not show anything to the user when this rule is violated. Code generation features generate code in this style, however. Rules with `none` severity never appear in the **Quick Actions and Refactorings** menu. In most cases, this is considered "disabled" or "ignored".
`silent` (also `refactoring` in Visual Studio 2017 version 15.8 and later) | Do not show anything to the user when this rule is violated. Code generation features generate code in this style, however. Rules with `silent` severity participate in cleanup as well as appear in the **Quick Actions and Refactorings** menu.
`suggestion` | When this style rule is violated, show it to the user as a suggestion. Suggestions appear as three gray dots under the first two characters.
`warning` | When this style rule is violated, show a compiler warning.
`error` | When this style rule is violated, show a compiler error.

## .NET code style settings

The style rules in this section are applicable to both C# and Visual Basic.

- ["This." and "Me." qualifiers](#this-and-me)
   - dotnet\_style\_qualification\_for_field
   - dotnet\_style\_qualification\_for_property
   - dotnet\_style\_qualification\_for_method
   - dotnet\_style\_qualification\_for_event
- [Language keywords instead of framework type names for type references](#language-keywords)
   - dotnet\_style\_predefined\_type\_for\_locals\_parameters_members
   - dotnet\_style\_predefined\_type\_for\_member_access
- [Modifier preferences](#normalize-modifiers)
   - dotnet\_style\_require\_accessibility_modifiers
   - csharp\_preferred\_modifier_order
   - visual\_basic\_preferred\_modifier_order
   - dotnet\_style\_readonly\_field
- [Parentheses preferences](#parentheses-preferences)
   - dotnet\_style\_parentheses\_in\_arithmetic\_binary\_operators
   - dotnet\_style\_parentheses\_in\_other\_binary\_operators
   - dotnet\_style\_parentheses\_in\_other\_operators
   - dotnet\_style\_parentheses\_in\_relational\_binary\_operators
- [Expression-level preferences](#expression-level-preferences)
   - dotnet\_style\_object_initializer
   - dotnet\_style\_collection_initializer
   - dotnet\_style\_explicit\_tuple_names
   - dotnet\_style\_prefer\_inferred\_tuple_names
   - dotnet\_style\_prefer\_inferred\_anonymous\_type\_member_names
   - dotnet\_style\_prefer\_auto\_properties
   - dotnet\_style\_prefer\_is\_null\_check\_over\_reference\_equality\_method
   - dotnet\_style\_prefer\_conditional\_expression\_over\_assignment
   - dotnet\_style\_prefer\_conditional\_expression\_over\_return
- ["Null" checking preferences](#null-checking-preferences)
   - dotnet\_style\_coalesce_expression
   - dotnet\_style\_null_propagation

### <a name="this-and-me"></a>"This." and "Me." qualifiers

This style rule can be applied to fields, properties, methods, or events. A value of **true** means prefer the code symbol to be prefaced with `this.` in C# or `Me.` in Visual Basic. A value of **false** means prefer the code element _not_ to be prefaced with `this.` or `Me.`.

These rules could appear in an *.editorconfig* file as follows:

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_qualification_for_field = false:suggestion
dotnet_style_qualification_for_property = false:suggestion
dotnet_style_qualification_for_method = false:suggestion
dotnet_style_qualification_for_event = false:suggestion
```

#### dotnet\_style\_qualification\_for_field

|||
|-|-|
| **Rule name** | dotnet_style_qualification_for_field |
| **Rule ID** | IDE0003 and IDE0009 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer fields to be prefaced with `this.` in C# or `Me.` in Visual Basic<br /><br />`false` - Prefer fields _not_ to be prefaced with `this.` or `Me.` |
| **Visual Studio default** | `false:silent` |

Code examples:

```csharp
// dotnet_style_qualification_for_field = true
this.capacity = 0;

// dotnet_style_qualification_for_field = false
capacity = 0;
```

```vb
' dotnet_style_qualification_for_field = true
Me.capacity = 0

' dotnet_style_qualification_for_field = false
capacity = 0
```

#### dotnet\_style\_qualification\_for_property

|||
|-|-|
| **Rule name** | dotnet_style_qualification_for_property |
| **Rule ID** | IDE0003 and IDE0009 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer properties to be prefaced with `this.` in C# or `Me.` in Visual Basic<br /><br />`false` - Prefer properties _not_ to be prefaced with `this.` or `Me.` |
| **Visual Studio default** | `false:silent` |

Code examples:

```csharp
// dotnet_style_qualification_for_property = true
this.ID = 0;

// dotnet_style_qualification_for_property = false
ID = 0;
```

```vb
' dotnet_style_qualification_for_property = true
Me.ID = 0

' dotnet_style_qualification_for_property = false
ID = 0
```

#### dotnet\_style\_qualification\_for_method

|||
|-|-|
| **Rule name** | dotnet_style_qualification_for_method |
| **Rule ID** | IDE0003 and IDE0009 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer methods to be prefaced with `this.` in C# or `Me.` in Visual Basic.<br /><br />`false` - Prefer methods _not_ to be prefaced with `this.` or `Me.`. |
| **Visual Studio default** | `false:silent` |

Code examples:

```csharp
// dotnet_style_qualification_for_method = true
this.Display();

// dotnet_style_qualification_for_method = false
Display();
```

```vb
' dotnet_style_qualification_for_method = true
Me.Display()

' dotnet_style_qualification_for_method = false
Display()
```

#### dotnet\_style\_qualification\_for_event

|||
|-|-|
| **Rule name** | dotnet_style_qualification_for_event |
| **Rule ID** | IDE0003 and IDE0009 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer events to be prefaced with `this.` in C# or `Me.` in Visual Basic.<br /><br />`false` - Prefer events _not_ to be prefaced with `this.` or `Me.`. |
| **Visual Studio default** | `false:silent` |

Code examples:

```csharp
// dotnet_style_qualification_for_event = true
this.Elapsed += Handler;

// dotnet_style_qualification_for_event = false
Elapsed += Handler;
```

```vb
' dotnet_style_qualification_for_event = true
AddHandler Me.Elapsed, AddressOf Handler

' dotnet_style_qualification_for_event = false
AddHandler Elapsed, AddressOf Handler
```

### <a name="language-keywords"></a>Language keywords instead of framework type names for type references

This style rule can be applied to local variables, method parameters, and class members, or as a separate rule to type member access expressions. A value of **true** means prefer the language keyword (for example, `int` or `Integer`) instead of the type name (for example, `Int32`) for types that have a keyword to represent them. A value of **false** means prefer the type name instead of the language keyword.

These rules could appear in an *.editorconfig* file as follows:

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_predefined_type_for_locals_parameters_members = true:suggestion
dotnet_style_predefined_type_for_member_access = true:suggestion
```

#### dotnet\_style\_predefined\_type\_for\_locals\_parameters_members

|||
|-|-|
| **Rule name** | dotnet_style_predefined_type_for_locals_parameters_members |
| **Rule ID** | IDE0012 and IDE0014 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer the language keyword for local variables, method parameters, and class members, instead of the type name, for types that have a keyword to represent them<br /><br />`false` - Prefer the type name for local variables, method parameters, and class members, instead of the language keyword |
| **Visual Studio default** | `true:silent` |

Code examples:

```csharp
// dotnet_style_predefined_type_for_locals_parameters_members = true
private int _member;

// dotnet_style_predefined_type_for_locals_parameters_members = false
private Int32 _member;
```

```vb
' dotnet_style_predefined_type_for_locals_parameters_members = true
Private _member As Integer

' dotnet_style_predefined_type_for_locals_parameters_members = false
Private _member As Int32
```

#### dotnet\_style\_predefined\_type\_for\_member_access

|||
|-|-|
| **Rule name** | dotnet_style_predefined_type_for_member_access |
| **Rule ID** | IDE0013 and IDE0015 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer the language keyword for member access expressions, instead of the type name, for types that have a keyword to represent them<br /><br />`false` - Prefer the type name for member access expressions, instead of the language keyword |
| **Visual Studio default** | `true:silent` |

Code examples:

```csharp
// dotnet_style_predefined_type_for_member_access = true
var local = int.MaxValue;

// dotnet_style_predefined_type_for_member_access = false
var local = Int32.MaxValue;
```

```vb
' dotnet_style_predefined_type_for_member_access = true
Dim local = Integer.MaxValue

' dotnet_style_predefined_type_for_member_access = false
Dim local = Int32.MaxValue
```

### <a name="normalize-modifiers"></a>Modifier preferences

The style rules in this section concern modifier preferences, including requiring accessibility modifiers, specifying the desired modifier sort order, and requiring the read-only modifier.

These rules could appear in an *.editorconfig* file as follows:

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_require_accessibility_modifiers = always:suggestion
dotnet_style_readonly_field = true:warning

# CSharp code style settings:
[*.cs]
csharp_preferred_modifier_order = public,private,protected,internal,static,extern,new,virtual,abstract,sealed,override,readonly,unsafe,volatile,async:suggestion

# Visual Basic code style settings:
[*.vb]
visual_basic_preferred_modifier_order = Partial,Default,Private,Protected,Public,Friend,NotOverridable,Overridable,MustOverride,Overloads,Overrides,MustInherit,NotInheritable,Static,Shared,Shadows,ReadOnly,WriteOnly,Dim,Const,WithEvents,Widening,Narrowing,Custom,Async:suggestion
```

#### dotnet\_style\_require\_accessibility_modifiers

|||
|-|-|
| **Rule name** | dotnet_style_require_accessibility_modifiers |
| **Rule ID** | IDE0040 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `always` - Prefer accessibility modifiers to be specified.<br /><br />`for_non_interface_members` - Prefer accessibility modifiers to be declared except for public interface members. (This is the same as **always** and has been added for future-proofing if C# adds default interface methods.)<br /><br />`never` - Do not prefer accessibility modifiers to be specified.<br /><br />`omit_if_default` - Prefer accessibility modifiers to be specified except if they are the default modifier. |
| **Visual Studio default** | `for_non_interface_members:silent` |
| **Introduced version** | Visual Studio 2017 version 15.5 |

Code examples:

```csharp
// dotnet_style_require_accessibility_modifiers = always
// dotnet_style_require_accessibility_modifiers = for_non_interface_members
class MyClass
{
    private const string thisFieldIsConst = "constant";
}

// dotnet_style_require_accessibility_modifiers = never
class MyClass
{
    const string thisFieldIsConst = "constant";
}
```

#### csharp_preferred_modifier_order

|||
|-|-|
| **Rule name** | csharp_preferred_modifier_order |
| **Rule ID** | IDE0036 |
| **Applicable languages** | C# |
| **Values** | One or more C# modifiers, such as `public`, `private`, and `protected` |
| **Visual Studio default** | `public, private, protected, internal, static, extern, new, virtual, abstract, sealed, override, readonly, unsafe, volatile, async:silent` |
| **Introduced version** | Visual Studio 2017 version 15.5 |

- When this rule is set to a list of modifiers, prefer the specified ordering.
- When this rule is omitted from the file, do not prefer a modifier order.

Code examples:

```csharp
// csharp_preferred_modifier_order = public,private,protected,internal,static,extern,new,virtual,abstract,sealed,override,readonly,unsafe,volatile,async
class MyClass
{
    private static readonly int _daysInYear = 365;
}
```

#### visual_basic_preferred_modifier_order

|||
|-|-|
| **Rule name** | visual_basic_preferred_modifier_order |
| **Rule ID** | IDE0036 |
| **Applicable languages** | Visual Basic |
| **Values** | One or more Visual Basic modifiers, such as `Partial`, `Private`, and `Public` |
| **Visual Studio default** | `Partial, Default, Private, Protected, Public, Friend, NotOverridable, Overridable, MustOverride, Overloads, Overrides, MustInherit, NotInheritable, Static, Shared, Shadows, ReadOnly, WriteOnly, Dim, Const,WithEvents, Widening, Narrowing, Custom, Async:silent` |
| **Introduced version** | Visual Studio 2017 version 15.5 |

- When this rule is set to a list of modifiers, prefer the specified ordering.
- When this rule is omitted from the file, do not prefer a modifier order.

Code examples:

```vb
' visual_basic_preferred_modifier_order = Partial,Default,Private,Protected,Public,Friend,NotOverridable,Overridable,MustOverride,Overloads,Overrides,MustInherit,NotInheritable,Static,Shared,Shadows,ReadOnly,WriteOnly,Dim,Const,WithEvents,Widening,Narrowing,Custom,Async
Public Class MyClass
    Private Shared ReadOnly daysInYear As Int = 365
End Class
```

#### dotnet_style_readonly_field

|||
|-|-|
| **Rule name** | dotnet_style_readonly_field |
| **Rule ID** | IDE0044 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer that fields should be marked with `readonly` (C#) or `ReadOnly` (Visual Basic) if they are only ever assigned inline, or inside of a constructor<br /><br />`false` - Specify no preference over whether fields should be marked with `readonly` (C#) or `ReadOnly` (Visual Basic) |
| **Visual Studio default** | `true:suggestion` |
| **Introduced version** | Visual Studio 2017 version 15.7 |

Code examples:

```csharp
// dotnet_style_readonly_field = true
class MyClass
{
    private readonly int _daysInYear = 365;
}
```

```vb
' dotnet_style_readonly_field = true
Public Class MyClass
    Private ReadOnly daysInYear As Int = 365
End Class
```

### Parentheses preferences

The style rules in this section concern parentheses preferences, including the use of parentheses for arithmetic, relational, and other binary operators.

These rules could appear in an *.editorconfig* file as follows:

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_parentheses_in_arithmetic_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_relational_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_other_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_other_operators = never_if_unnecessary:silent
```

#### dotnet\_style\_parentheses\_in\_arithmetic\_binary_operators

|||
|-|-|
| **Rule name** | dotnet_style_parentheses_in_arithmetic_binary_operators |
| **Rule ID** | IDE0047 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `always_for_clarity` - Prefer parentheses to clarify arithmetic operator (`*`, `/`, `%`, `+`, `-`, `<<`, `>>`, `&`, `^`, `|`) precedence<br /><br />`never_if_unnecessary` - Prefer to not have parentheses when arithmetic operator (`*`, `/`, `%`, `+`, `-`, `<<`, `>>`, `&`, `^`, `|`) precedence is obvious |
| **Visual Studio default** | `always_for_clarity:silent` |
| **Introduced version** | Visual Studio 2017 version 15.8 |

Code examples:

```csharp
// dotnet_style_parentheses_in_arithmetic_binary_operators = always_for_clarity
var v = a + (b * c);

// dotnet_style_parentheses_in_arithmetic_binary_operators = never_if_unnecessary
var v = a + b * c;
```

```vb
' dotnet_style_parentheses_in_arithmetic_binary_operators = always_for_clarity
Dim v = a + (b * c)

' dotnet_style_parentheses_in_arithmetic_binary_operators = never_if_unnecessary
Dim v = a + b * c
```

#### dotnet\_style\_parentheses\_in\_relational\_binary_operators

|||
|-|-|
| **Rule name** | dotnet_style_parentheses_in_relational_binary_operators |
| **Rule ID** | IDE0047 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `always_for_clarity` - Prefer parentheses to clarify relational operator (`>`, `<`, `<=`, `>=`, `is`, `as`, `==`, `!=`) precedence<br /><br />`never_if_unnecessary` - Prefer to not have parentheses when relational operator (`>`, `<`, `<=`, `>=`, `is`, `as`, `==`, `!=`) precedence is obvious |
| **Visual Studio default** | `always_for_clarity:silent` |
| **Introduced version** | Visual Studio 2017 version 15.8 |

Code examples:

```csharp
// dotnet_style_parentheses_in_relational_binary_operators = always_for_clarity
var v = (a < b) == (c > d);

// dotnet_style_parentheses_in_relational_binary_operators = never_if_unnecessary
var v = a < b == c > d;
```

```vb
' dotnet_style_parentheses_in_relational_binary_operators = always_for_clarity
Dim v = (a < b) = (c > d)

' dotnet_style_parentheses_in_relational_binary_operators = never_if_unnecessary
Dim v = a < b = c > d
```

#### dotnet\_style\_parentheses\_in\_other\_binary_operators

|||
|-|-|
| **Rule name** | dotnet_style_parentheses_in_other_binary_operators |
| **Rule ID** | IDE0047 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `always_for_clarity` - Prefer parentheses to clarify other binary operator (`&&`, `||`, `??`) precedence<br /><br />`never_if_unnecessary` - Prefer to not have parentheses when other binary operator (`&&`, `||`, `??`) precedence is obvious |
| **Visual Studio default** | `always_for_clarity:silent` |
| **Introduced version** | Visual Studio 2017 version 15.8 |

Code examples:

```csharp
// dotnet_style_parentheses_in_other_binary_operators = always_for_clarity
var v = a || (b && c);

// dotnet_style_parentheses_in_other_binary_operators = never_if_unnecessary
var v = a || b && c;
```

```vb
' dotnet_style_parentheses_in_other_binary_operators = always_for_clarity
Dim v = a OrElse (b AndAlso c)

' dotnet_style_parentheses_in_other_binary_operators = never_if_unnecessary
Dim v = a OrElse b AndAlso c
```

#### dotnet\_style\_parentheses\_in\_other_operators

|||
|-|-|
| **Rule name** | dotnet_style_parentheses_in_other_operators |
| **Rule ID** | IDE0047 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `always_for_clarity` - Prefer parentheses to clarify operator precedence<br /><br />`never_if_unnecessary` - Prefer to not have parentheses when operator precedence is obvious |
| **Visual Studio default** | `never_if_unnecessary:silent` |
| **Introduced version** | Visual Studio 2017 version 15.8 |

Code examples:

```csharp
// dotnet_style_parentheses_in_other_operators = always_for_clarity
var v = (a.b).Length;

// dotnet_style_parentheses_in_other_operators = never_if_unnecessary
var v = a.b.Length;
```

```vb
' dotnet_style_parentheses_in_other_operators = always_for_clarity
Dim v = (a.b).Length

' dotnet_style_parentheses_in_other_operators = never_if_unnecessary
Dim v = a.b.Length
```

### Expression-level preferences

The style rules in this section concern expression-level preferences, including the use of object initializers, collection initializers, explicit or inferred tuple names, and inferred anonymous types.

These rules could appear in an *.editorconfig* file as follows:

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_object_initializer = true:suggestion
dotnet_style_collection_initializer = true:suggestion
dotnet_style_explicit_tuple_names = true:suggestion
dotnet_style_prefer_inferred_tuple_names = true:suggestion
dotnet_style_prefer_inferred_anonymous_type_member_names = true:suggestion
dotnet_style_prefer_auto_properties = true:silent
dotnet_style_prefer_conditional_expression_over_assignment = true:suggestion
dotnet_style_prefer_conditional_expression_over_return = true:suggestion
```

#### dotnet\_style\_object_initializer

|||
|-|-|
| **Rule name** | dotnet_style_object_initializer |
| **Rule ID** | IDE0017 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer objects to be initialized using object initializers when possible<br /><br />`false` - Prefer objects to *not* be initialized using object initializers |
| **Visual Studio default** | `true:suggestion` |

Code examples:

```csharp
// dotnet_style_object_initializer = true
var c = new Customer() { Age = 21 };

// dotnet_style_object_initializer = false
var c = new Customer();
c.Age = 21;
```

```vb
' dotnet_style_object_initializer = true
Dim c = New Customer() With {.Age = 21}

' dotnet_style_object_initializer = false
Dim c = New Customer()
c.Age = 21
```

#### dotnet\_style\_collection_initializer

|||
|-|-|
| **Rule name** | dotnet_style_collection_initializer |
| **Rule ID** | IDE0028 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer collections to be initialized using collection initializers when possible<br /><br />`false` - Prefer collections to *not* be initialized using collection initializers |
| **Visual Studio default** | `true:suggestion` |

Code examples:

```csharp
// dotnet_style_collection_initializer = true
var list = new List<int> { 1, 2, 3 };

// dotnet_style_collection_initializer = false
var list = new List<int>();
list.Add(1);
list.Add(2);
list.Add(3);
```

```vb
' dotnet_style_collection_initializer = true
Dim list = New List(Of Integer) From {1, 2, 3}

' dotnet_style_collection_initializer = false
Dim list = New List(Of Integer)
list.Add(1)
list.Add(2)
list.Add(3)
```

#### dotnet\_style\_explicit\_tuple_names

|||
|-|-|
| **Rule name** | dotnet_style_explicit_tuple_names |
| **Rule ID** | IDE0033 |
| **Applicable languages** | C# 7.0+ and Visual Basic 15+ |
| **Values** | `true` - Prefer tuple names to ItemX properties<br /><br />`false` - Prefer ItemX properties to tuple names |
| **Visual Studio default** | `true:suggestion` |

Code examples:

```csharp
// dotnet_style_explicit_tuple_names = true
(string name, int age) customer = GetCustomer();
var name = customer.name;

// dotnet_style_explicit_tuple_names = false
(string name, int age) customer = GetCustomer();
var name = customer.Item1;
```

```vb
 ' dotnet_style_explicit_tuple_names = true
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.name

' dotnet_style_explicit_tuple_names = false
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.Item1
```

#### dotnet\_style\_prefer\_inferred\_tuple_names

|||
|-|-|
| **Rule name** | dotnet_style_prefer_inferred_tuple_names |
| **Rule ID** | IDE0037 |
| **Applicable languages** | C# 7.1+ and Visual Basic 15+ |
| **Values** | `true` - Prefer inferred tuple element names<br /><br />`false` - Prefer explicit tuple element names |
| **Visual Studio default** | `true:suggestion` |
| **Introduced version** | Visual Studio 2017 version 15.6 |

Code examples:

```csharp
// dotnet_style_prefer_inferred_tuple_names = true
var tuple = (age, name);

// dotnet_style_prefer_inferred_tuple_names = false
var tuple = (age: age, name: name);
```

```vb
' dotnet_style_prefer_inferred_tuple_names = true
Dim tuple = (name, age)

' dotnet_style_prefer_inferred_tuple_names = false
Dim tuple = (name:=name, age:=age)
```

#### dotnet\_style\_prefer\_inferred\_anonymous\_type\_member_names

|||
|-|-|
| **Rule name** | dotnet_style_prefer_inferred_anonymous_type_member_names |
| **Rule ID** | IDE0037 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer inferred anonymous type member names<br /><br />`false` - Prefer explicit anonymous type member names |
| **Visual Studio default** | `true:suggestion` |
| **Introduced version** | Visual Studio 2017 version 15.6 |

Code examples:

```csharp
// dotnet_style_prefer_inferred_anonymous_type_member_names = true
var anon = new { age, name };

// dotnet_style_prefer_inferred_anonymous_type_member_names = false
var anon = new { age = age, name = name };
```

```vb
' dotnet_style_prefer_inferred_anonymous_type_member_names = true
Dim anon = New With {name, age}

' dotnet_style_prefer_inferred_anonymous_type_member_names = false
Dim anon = New With {.name = name, .age = age}
```

#### dotnet\_style\_prefer\_auto\_properties

|||
|-|-|
| **Rule name** | dotnet_style_prefer_auto_properties |
| **Rule ID** | IDE0032 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer autoproperties over properties with private backing fields<br /><br />`false` - Prefer properties with private backing fields over autoproperties |
| **Visual Studio default** | `true:suggestion` |
| **Introduced version** | Visual Studio 2017 version 15.7 |

Code examples:

```csharp
// dotnet_style_prefer_auto_properties = true
private int Age { get; }

// dotnet_style_prefer_auto_properties = false
private int age;

public int Age
{
    get
    {
        return age;
    }
}
```

```vb
' dotnet_style_prefer_auto_properties = true
Public ReadOnly Property Age As Integer

' dotnet_style_prefer_auto_properties = false
Private _age As Integer

Public ReadOnly Property Age As Integer
    Get
        return _age
    End Get
End Property
```

#### dotnet\_style\_prefer\_is\_null\_check\_over\_reference\_equality\_method

|||
|-|-|
| **Rule name** | dotnet_style_prefer_is_null_check_over_reference_equality_method |
| **Rule ID** | IDE0041 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer using a null check with pattern-matching over `object.ReferenceEquals`<br /><br />`false` - Prefer `object.ReferenceEquals` over a null check with pattern-matching |
| **Visual Studio default** | `true:suggestion` |
| **Introduced version** | Visual Studio 2017 version 15.7 |

Code examples:

```csharp
// dotnet_style_prefer_is_null_check_over_reference_equality_method = true
if (value is null)
    return;

// dotnet_style_prefer_is_null_check_over_reference_equality_method = false
if (object.ReferenceEquals(value, null))
    return;
```

```vb
' dotnet_style_prefer_is_null_check_over_reference_equality_method = true
If value Is Nothing
    Return
End If

' dotnet_style_prefer_is_null_check_over_reference_equality_method = false
If Object.ReferenceEquals(value, Nothing)
    Return
End If
```

#### dotnet\_style\_prefer\_conditional\_expression\_over_assignment

|||
|-|-|
| **Rule name** | dotnet_style_prefer_conditional_expression_over_assignment |
| **Rule ID** | IDE0045 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer assignments with a ternary conditional over an if-else statement<br /><br />`false` - Prefer assignments with an if-else statement over a ternary conditional |
| **Visual Studio default** | `true:suggestion` |
| **Introduced version** | Visual Studio 2017 version 15.8 |

Code examples:

```csharp
// dotnet_style_prefer_conditional_expression_over_assignment = true
string s = expr ? "hello" : "world";

// dotnet_style_prefer_conditional_expression_over_assignment = false
string s;
if (expr)
{
    s = "hello";
}
else
{
    s = "world";
}
```

```vb
' dotnet_style_prefer_conditional_expression_over_assignment = true
Dim s As String = If(expr, "hello", "world")

' dotnet_style_prefer_conditional_expression_over_assignment = false
Dim s As String
If expr Then
    s = "hello"
Else
    s = "world"
End If
```

#### dotnet\_style\_prefer\_conditional\_expression\_over_return

|||
|-|-|
| **Rule name** | dotnet_style_prefer_conditional_expression_over_return |
| **Rule ID** | IDE0046 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer return statements to use a ternary conditional over an if-else statement<br /><br />`false` - Prefer return statements to use an if-else statement over a ternary conditional |
| **Visual Studio default** | `true:suggestion` |
| **Introduced version** | Visual Studio 2017 version 15.8 |

Code examples:

```csharp
// dotnet_style_prefer_conditional_expression_over_return = true
return expr ? "hello" : "world"

// dotnet_style_prefer_conditional_expression_over_return = false
if (expr)
{
    return "hello";
}
else
{
    return "world";
}
```

```vb
' dotnet_style_prefer_conditional_expression_over_return = true
Return If(expr, "hello", "world")

' dotnet_style_prefer_conditional_expression_over_return = false
If expr Then
    Return "hello"
Else
    Return "world"
End If
```

### Null-checking preferences

The style rules in this section concern null-checking preferences.

These rules could appear in an *.editorconfig* file as follows:

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_coalesce_expression = true:suggestion
dotnet_style_null_propagation = true:suggestion
```

#### dotnet\_style\_coalesce_expression

|||
|-|-|
| **Rule name** | dotnet_style_coalesce_expression |
| **Rule ID** | IDE0029 |
| **Applicable languages** | C# and Visual Basic |
| **Values** | `true` - Prefer null coalescing expressions to ternary operator checking<br /><br />`false` - Prefer ternary operator checking to null coalescing expressions |
| **Visual Studio default** | `true:suggestion` |

Code examples:

```csharp
// dotnet_style_coalesce_expression = true
var v = x ?? y;

// dotnet_style_coalesce_expression = false
var v = x != null ? x : y; // or
var v = x == null ? y : x;
```

```vb
' dotnet_style_coalesce_expression = true
Dim v = If(x, y)

' dotnet_style_coalesce_expression = false
Dim v = If(x Is Nothing, y, x) ' or
Dim v = If(x IsNot Nothing, x, y)
```

#### dotnet\_style\_null_propagation

|||
|-|-|
| **Rule name** | dotnet_style_null_propagation |
| **Rule ID** | IDE0031 |
| **Applicable languages** | C# 6.0+ and Visual Basic 14+ |
| **Values** | `true` - Prefer to use null-conditional operator when possible<br /><br />`false` - Prefer to use ternary null checking where possible |
| **Visual Studio default** | `true:suggestion` |

Code examples:

```csharp
// dotnet_style_null_propagation = true
var v = o?.ToString();

// dotnet_style_null_propagation = false
var v = o == null ? null : o.ToString(); // or
var v = o != null ? o.String() : null;
```

```vb
' dotnet_style_null_propagation = true
Dim v = o?.ToString()

' dotnet_style_null_propagation = false
Dim v = If(o Is Nothing, Nothing, o.ToString()) ' or
Dim v = If(o IsNot Nothing, o.ToString(), Nothing)
```

## C# code style settings

The style rules in this section are applicable to C# only.

- [Implicit and explicit types](#implicit-and-explicit-types)
   - csharp\_style\_var\_for\_built\_in_types
   - csharp\_style\_var\_when\_type\_is_apparent
   - csharp\_style\_var_elsewhere
- [Expression-bodied members](#expression-bodied-members)
   - csharp\_style\_expression\_bodied_methods
   - csharp\_style\_expression\_bodied_constructors
   - csharp\_style\_expression\_bodied_operators
   - csharp\_style\_expression\_bodied_properties
   - csharp\_style\_expression\_bodied_indexers
   - csharp\_style\_expression\_bodied_accessors
- [Pattern matching](#pattern-matching)
   - csharp\_style\_pattern\_matching\_over\_is\_with\_cast_check
   - csharp\_style\_pattern\_matching\_over\_as\_with\_null_check
- [Inlined variable declarations](#inlined-variable-declarations)
   - csharp\_style\_inlined\_variable_declaration
- [Expression-level preferences](#expression-level-preferences)
   - csharp\_prefer\_simple\_default_expression
   - csharp\_style\_deconstructed\_variable_declaration
   - csharp\_style\_pattern\_local\_over\_anonymous_function
- ["Null" checking preferences](#null-checking-preferences)
   - csharp\_style\_throw_expression
   - csharp\_style\_conditional\_delegate_call
- [Code block preferences](#code-block-preferences)
   - csharp\_prefer_braces

### Implicit and explicit types

The style rules in this section concern the use of the [var](/dotnet/csharp/language-reference/keywords/var) keyword versus an explicit type in a variable declaration. This rule can be applied separately to built-in types, when the type is apparent, and elsewhere.

Example *.editorconfig* file:

```ini
# CSharp code style settings:
[*.cs]
csharp_style_var_for_built_in_types = true:suggestion
csharp_style_var_when_type_is_apparent = true:suggestion
csharp_style_var_elsewhere = true:suggestion
```

#### csharp\_style\_var\_for\_built\_in_types

|||
|-|-|
| **Rule name** | csharp_style_var_for_built_in_types |
| **Rule ID** | IDE0007 and IDE0008 |
| **Applicable languages** | C#  |
| **Values** | `true` - Prefer `var` is used to declare variables with built-in system types such as `int`<br /><br />`false` - Prefer explicit type over `var` to declare variables with built-in system types such as `int` |
| **Visual Studio default** | `true:silent` |

Code examples:

```csharp
// csharp_style_var_for_built_in_types = true
var x = 5;

// csharp_style_var_for_built_in_types = false
int x = 5;
```

#### csharp\_style\_var\_when\_type\_is_apparent

|||
|-|-|
| **Rule name** | csharp_style_var_when_type_is_apparent |
| **Rule ID** | IDE0007 and IDE0008 |
| **Applicable languages** | C#  |
| **Values** | `true` - Prefer `var` when the type is already mentioned on the right-hand side of a declaration expression<br /><br />`false` - Prefer explicit type over `var` when the type is already mentioned on the right-hand side of a declaration expression |
| **Visual Studio default** | `true:silent` |

Code examples:

```csharp
// csharp_style_var_when_type_is_apparent = true
var obj = new Customer();

// csharp_style_var_when_type_is_apparent = false
Customer obj = new Customer();
```

#### csharp\_style\_var_elsewhere

|||
|-|-|
| **Rule name** | csharp_style_var_elsewhere |
| **Rule ID** | IDE0007 and IDE0008 |
| **Applicable languages** | C#  |
| **Values** | `true` - Prefer `var` over explicit type in all cases, unless overridden by another code style rule<br /><br />`false` - Prefer explicit type over `var` in all cases, unless overridden by another code style rule |
| **Visual Studio default** | `true:silent` |

Code examples:

```csharp
// csharp_style_var_elsewhere = true
var f = this.Init();

// csharp_style_var_elsewhere = false
bool f = this.Init();
```

### Expression-bodied members

The style rules in this section concern the use of [expression-bodied members](/dotnet/csharp/programming-guide/statements-expressions-operators/expression-bodied-members) when the logic consists of a single expression. This rule can be applied to methods, constructors, operators, properties, indexers, and accessors.

Example *.editorconfig* file:

```ini
# CSharp code style settings:
[*.cs]
csharp_style_expression_bodied_methods = false:silent
csharp_style_expression_bodied_constructors = false:silent
csharp_style_expression_bodied_operators = false:silent
csharp_style_expression_bodied_properties = true:suggestion
csharp_style_expression_bodied_indexers = true:suggestion
csharp_style_expression_bodied_accessors = true:suggestion
```

#### csharp\_style\_expression\_bodied_methods

|||
|-|-|
| **Rule name** | csharp_style_expression_bodied_methods |
| **Rule ID** | IDE0022 |
| **Applicable languages** | C# 6.0+  |
| **Values** | `true` - Prefer expression-bodied members for methods<br /><br />`when_on_single_line` - Prefer expression-bodied members for methods when they will be a single line<br /><br />`false` - Prefer block bodies for methods |
| **Visual Studio default** | `false:silent` |

Code examples:

```csharp
// csharp_style_expression_bodied_methods = true
public int GetAge() => this.Age;

// csharp_style_expression_bodied_methods = false
public int GetAge() { return this.Age; }
```

#### csharp\_style\_expression\_bodied_constructors

|||
|-|-|
| **Rule name** | csharp_style_expression_bodied_constructors |
| **Rule ID** | IDE0021 |
| **Applicable languages** | C# 7.0+  |
| **Values** | `true` - Prefer expression-bodied members for constructors<br /><br />`when_on_single_line` - Prefer expression-bodied members for constructors when they will be a single line<br /><br />`false` - Prefer block bodies for constructors |
| **Visual Studio default** | `false:silent` |

Code examples:

```csharp
// csharp_style_expression_bodied_constructors = true
public Customer(int age) => Age = age;

// csharp_style_expression_bodied_constructors = false
public Customer(int age) { Age = age; }
```

#### csharp\_style\_expression\_bodied_operators

|||
|-|-|
| **Rule name** | csharp_style_expression_bodied_operators |
| **Rule ID** | IDE0023 and IDE0024 |
| **Applicable languages** | C# 7.0+  |
| **Values** | `true` - Prefer expression-bodied members for operators<br /><br />`when_on_single_line` - Prefer expression-bodied members for operators when they will be a single line<br /><br />`false` - Prefer block bodies for operators |
| **Visual Studio default** | `false:silent` |

Code examples:

```csharp
// csharp_style_expression_bodied_operators = true
public static ComplexNumber operator + (ComplexNumber c1, ComplexNumber c2)
    => new ComplexNumber(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary);

// csharp_style_expression_bodied_operators = false
public static ComplexNumber operator + (ComplexNumber c1, ComplexNumber c2)
{ return new ComplexNumber(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary); }
```

#### csharp\_style\_expression\_bodied_properties

|||
|-|-|
| **Rule name** | csharp_style_expression_bodied_properties |
| **Rule ID** | IDE0025 |
| **Applicable languages** | C# 7.0+  |
| **Values** | `true` - Prefer expression-bodied members for properties<br /><br />`when_on_single_line` - Prefer expression-bodied members for properties when they will be a single line<br /><br />`false` - Prefer block bodies for properties |
| **Visual Studio default** | `true:silent` |

Code examples:

```csharp
// csharp_style_expression_bodied_properties = true
public int Age => _age;

// csharp_style_expression_bodied_properties = false
public int Age { get { return _age; }}
```

#### csharp\_style\_expression\_bodied_indexers

|||
|-|-|
| **Rule name** | csharp_style_expression_bodied_indexers |
| **Rule ID** | IDE0026 |
| **Applicable languages** | C# 7.0+  |
| **Values** | `true` - Prefer expression-bodied members for indexers<br /><br />`when_on_single_line` - Prefer expression-bodied members for indexers when they will be a single line<br /><br />`false` - Prefer block bodies for indexers |
| **Visual Studio default** | `true:silent` |

Code examples:

```csharp
// csharp_style_expression_bodied_indexers = true
public T this[int i] => _values[i];

// csharp_style_expression_bodied_indexers = false
public T this[int i] { get { return _values[i]; } }
```

#### csharp\_style\_expression\_bodied_accessors

|||
|-|-|
| **Rule name** | csharp_style_expression_bodied_accessors |
| **Rule ID** | IDE0027 |
| **Applicable languages** | C# 7.0+  |
| **Values** | `true` - Prefer expression-bodied members for accessors<br /><br />`when_on_single_line` - Prefer expression-bodied members for accessors when they will be a single line<br /><br />`false` - Prefer block bodies for accessors |
| **Visual Studio default** | `true:silent` |

Code examples:

```csharp
// csharp_style_expression_bodied_accessors = true
public int Age { get => _age; set => _age = value; }

// csharp_style_expression_bodied_accessors = false
public int Age { get { return _age; } set { _age = value; } }
```

### Pattern matching

The style rules in this section concern the use of [pattern matching](/dotnet/csharp/pattern-matching) in C#.

Example *.editorconfig* file:

```ini
# CSharp code style settings:
[*.cs]
csharp_style_pattern_matching_over_is_with_cast_check = true:suggestion
csharp_style_pattern_matching_over_as_with_null_check = true:suggestion
```

#### csharp\_style\_pattern\_matching\_over\_is\_with\_cast_check

|||
|-|-|
| **Rule name** | csharp_style_pattern_matching_over_is_with_cast_check |
| **Rule ID** | IDE0020 |
| **Applicable languages** | C# 7.0+  |
| **Values** | `true` - Prefer pattern matching instead of `is` expressions with type casts<br /><br />`false` - Prefer `is` expressions with type casts instead of pattern matching |
| **Visual Studio default** | `true:suggestion` |

Code examples:

```csharp
// csharp_style_pattern_matching_over_is_with_cast_check = true
if (o is int i) {...}

// csharp_style_pattern_matching_over_is_with_cast_check = false
if (o is int) {var i = (int)o; ... }
```

#### csharp\_style\_pattern\_matching\_over\_as\_with\_null_check

|||
|-|-|
| **Rule name** | csharp_style_pattern_matching_over_as_with_null_check |
| **Rule ID** | IDE0019 |
| **Applicable languages** | C# 7.0+  |
| **Values** | `true` - Prefer pattern matching instead of `as` expressions with null checks to determine if something is of a particular type<br /><br />`false` - Prefer `as` expressions with null checks instead of pattern matching to determine if something is of a particular type |
| **Visual Studio default** | `true:suggestion` |

Code examples:

```csharp
// csharp_style_pattern_matching_over_as_with_null_check = true
if (o is string s) {...}

// csharp_style_pattern_matching_over_as_with_null_check = false
var s = o as string;
if (s != null) {...}
```

### Inlined variable declarations

This style rule concerns whether `out` variables are declared inline or not. Starting in C# 7, you can [declare an out variable in the argument list of a method call](/dotnet/csharp/language-reference/keywords/out-parameter-modifier#calling-a-method-with-an-out-argument), rather than in a separate variable declaration.

#### csharp\_style\_inlined\_variable_declaration

|||
|-|-|
| **Rule name** | csharp_style_inlined_variable_declaration |
| **Rule ID** | IDE0018 |
| **Applicable languages** | C# 7.0+  |
| **Values** | `true` - Prefer `out` variables to be declared inline in the argument list of a method call when possible<br /><br />`false` - Prefer `out` variables to be declared before the method call |
| **Visual Studio default** | `true:suggestion` |

Code examples:

```csharp
// csharp_style_inlined_variable_declaration = true
if (int.TryParse(value, out int i) {...}

// csharp_style_inlined_variable_declaration = false
int i;
if (int.TryParse(value, out i) {...}
```

Example *.editorconfig* file:

```ini
# CSharp code style settings:
[*.cs]
csharp_style_inlined_variable_declaration = true:suggestion
```

### Expression-level preferences

The style rules in this section concern expression-level preferences, including the use of [default expressions](/dotnet/csharp/programming-guide/statements-expressions-operators/default-value-expressions#default-literal-and-type-inference), deconstructed variables, and local functions over anonymous functions.

Example *.editorconfig* file:

```ini
# CSharp code style settings:
[*.cs]
csharp_prefer_simple_default_expression = true:suggestion
csharp_style_deconstructed_variable_declaration = true:suggestion
csharp_style_pattern_local_over_anonymous_function = true:suggestion
```

#### csharp\_prefer\_simple\_default_expression

This style rule concerns using the [`default` literal for default value expressions](/dotnet/csharp/programming-guide/statements-expressions-operators/default-value-expressions#default-literal-and-type-inference) when the compiler can infer the type of the expression.

|||
|-|-|
| **Rule name** | csharp_prefer_simple_default_expression |
| **Rule ID** | IDE0034 |
| **Applicable languages** | C# 7.1+  |
| **Values** | `true` - Prefer `default` over `default(T)`<br /><br />`false` - Prefer `default(T)` over `default` |
| **Visual Studio default** | `true:suggestion` |

Code examples:

```csharp
// csharp_prefer_simple_default_expression = true
void DoWork(CancellationToken cancellationToken = default) { ... }

// csharp_prefer_simple_default_expression = false
void DoWork(CancellationToken cancellationToken = default(CancellationToken)) { ... }
```

#### csharp\_style\_deconstructed\_variable_declaration

|||
|-|-|
| **Rule name** | csharp_style_deconstructed_variable_declaration |
| **Rule ID** | IDE0042 |
| **Applicable languages** | C# 7.0+  |
| **Values** | `true` - Prefer deconstructed variable declaration<br /><br />`false` - Do not prefer deconstruction in variable declarations |
| **Visual Studio default** | `true:suggestion` |

Code examples:

```csharp
// csharp_style_deconstructed_variable_declaration = true
var (name, age) = GetPersonTuple();
Console.WriteLine($"{name} {age}");

(int x, int y) = GetPointTuple();
Console.WriteLine($"{x} {y}");

// csharp_style_deconstructed_variable_declaration = false
var person = GetPersonTuple();
Console.WriteLine($"{person.name} {person.age}");

(int x, int y) point = GetPointTuple();
Console.WriteLine($"{point.x} {point.y}");
```

#### csharp\_style\_pattern\_local\_over\_anonymous_function

|||
|-|-|
| **Rule name** | csharp_style_pattern_local_over_anonymous_function |
| **Rule ID** | IDE0039 |
| **Applicable languages** | C# 7.0+  |
| **Values** | `true` - Prefer local functions over anonymous functions<br /><br />`false` - Prefer anonymous functions over local functions |
| **Visual Studio default** | `true:suggestion` |

Code examples:

```csharp
// csharp_style_pattern_local_over_anonymous_function = true
int fibonacci(int n)
{
    return n <= 1 ? 1 : fibonacci(n-1) + fibonacci(n-2);
}

// csharp_style_pattern_local_over_anonymous_function = false
Func<int, int> fibonacci = null;
fibonacci = (int n) =>
{
    return n <= 1 ? 1 : fibonacci(n - 1) + fibonacci(n - 2);
};
```

### Null-checking preferences

These style rules concern the syntax around `null` checking, including using `throw` expressions or `throw` statements, and whether to perform a null check or use the conditional coalescing operator (`?.`) when invoking a [lambda expression](/dotnet/csharp/lambda-expressions).

Example *.editorconfig* file:

```ini
# CSharp code style settings:
[*.cs]
csharp_style_throw_expression = true:suggestion
csharp_style_conditional_delegate_call = false:suggestion
```

#### csharp\_style\_throw_expression

|||
|-|-|
| **Rule name** | csharp_style_throw_expression |
| **Rule ID** | IDE0016 |
| **Applicable languages** | C# 7.0+  |
| **Values** | `true` - Prefer to use `throw` expressions instead of `throw` statements<br /><br />`false` - Prefer to use `throw` statements instead of `throw` expressions |
| **Visual Studio default** | `true:suggestion` |

Code examples:

```csharp
// csharp_style_throw_expression = true
this.s = s ?? throw new ArgumentNullException(nameof(s));

// csharp_style_throw_expression = false
if (s == null) { throw new ArgumentNullException(nameof(s)); }
this.s = s;
```

#### csharp\_style\_conditional\_delegate_call

|||
|-|-|
| **Rule name** | csharp_style_conditional_delegate_call |
| **Rule ID** | IDE0041 |
| **Applicable languages** | C# 6.0+  |
| **Values** | `true` - refer to use the conditional coalescing operator (`?.`) when invoking a lambda expression, instead of performing a null check<br /><br />`false` - Prefer to perform a null check before invoking a lambda expression, instead of using the conditional coalescing operator (`?.`) |
| **Visual Studio default** | `true:suggestion` |

Code examples:

```csharp
// csharp_style_conditional_delegate_call = true
func?.Invoke(args);

// csharp_style_conditional_delegate_call = false
if (func != null) { func(args); }
```

### Code block preferences

This style rule concerns the use of curly braces `{ }` to surround code blocks.

Example *.editorconfig* file:

```ini
# CSharp code style settings:
[*.cs]
csharp_prefer_braces = true:silent
```

#### csharp\_prefer\_braces

|||
|-|-|
| **Rule name** | csharp_prefer_braces |
| **Rule ID** | IDE0011 |
| **Applicable languages** | C# |
| **Values** | `true` - Prefer curly braces even for one line of code<br /><br />`false` - Prefer no curly braces if allowed |
| **Visual Studio default** | `true:silent` |

Code examples:

```csharp
// csharp_prefer_braces = true
if (test) { this.Display(); }

// csharp_prefer_braces = false
if (test) this.Display();
```

## See also

- [Formatting conventions](editorconfig-formatting-conventions.md)
- [Naming conventions](editorconfig-naming-conventions.md)
- [.NET coding convention settings for EditorConfig](editorconfig-code-style-settings-reference.md)