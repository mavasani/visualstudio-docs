---
title: "CA1708: Identifiers should differ by more than case"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "IdentifiersShouldDifferByMoreThanCase"
  - "CA1708"
helpviewer_keywords:
  - "CA1708"
  - "IdentifiersShouldDifferByMoreThanCase"
ms.assetid: dac0f01d-dd21-484d-add1-c8cd2bf6969f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1708: Identifiers should differ by more than case

|||
|-|-|
|TypeName|IdentifiersShouldDifferByMoreThanCase|
|CheckId|CA1708|
|Category|Microsoft.Naming|
|Breaking Change|Breaking|

## Cause

The names of two types, members, parameters, or fully qualified namespaces are identical when they're converted to lowercase.

By default, this rule only looks at externally visible types, members, and namespaces, but this is [configurable](#configurability).

## Rule description

Identifiers for namespaces, types, members, and parameters cannot differ only by case because languages that target the common language runtime are not required to be case-sensitive. For example, [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] is a widely used case-insensitive language.

This rule fires on publicly visible members only.

## How to fix violations

Select a name that is unique when it is compared to other identifiers in a case-insensitive manner.

## When to suppress warnings

Do not suppress a warning from this rule. The library might not be usable in all available languages in .NET.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1708.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Naming). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Example of a violation

The following example demonstrates a violation of this rule.

[!code-csharp[FxCop.Naming.IdentifiersShouldDifferByMoreThanCase#1](../code-quality/codesnippet/CSharp/ca1708-identifiers-should-differ-by-more-than-case_1.cs)]

## Related rules

- [CA1709: Identifiers should be cased correctly](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)