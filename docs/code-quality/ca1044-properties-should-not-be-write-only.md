---
title: "CA1044: Properties should not be write only"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "PropertiesShouldNotBeWriteOnly"
  - "CA1044"
helpviewer_keywords:
  - "CA1044"
  - "PropertiesShouldNotBeWriteOnly"
ms.assetid: 8386bf3a-b161-4841-bf8b-92591595aea9
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1044: Properties should not be write only

|||
|-|-|
|TypeName|PropertiesShouldNotBeWriteOnly|
|CheckId|CA1044|
|Category|Microsoft.Design|
|Breaking Change|Breaking|

## Cause

A property has a set accessor but not a get accessor.

By default, this rule only looks at public types, but this is [configurable](#configurability).

## Rule description

Get accessors provide read access to a property and set accessors provide write access. Although it is acceptable and often necessary to have a read-only property, the design guidelines prohibit the use of write-only properties. This is because letting a user set a value and then preventing the user from viewing the value does not provide any security. Also, without read access, the state of shared objects cannot be viewed, which limits their usefulness.

## How to fix violations

To fix a violation of this rule, add a get accessor to the property. Alternatively, if the behavior of a write-only property is necessary, consider converting this property to a method.

## When to suppress warnings

It is recommended that you do not suppress warnings from this rule.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1044.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Design). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Example

In the following example, `BadClassWithWriteOnlyProperty` is a type with a write-only property. `GoodClassWithReadWriteProperty` contains the corrected code.

[!code-vb[FxCop.Design.PropertiesNotWriteOnly#1](../code-quality/codesnippet/VisualBasic/ca1044-properties-should-not-be-write-only_1.vb)]
[!code-csharp[FxCop.Design.PropertiesNotWriteOnly#1](../code-quality/codesnippet/CSharp/ca1044-properties-should-not-be-write-only_1.cs)]