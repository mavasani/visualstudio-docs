---
title: "CA1801: Review unused parameters"
ms.date: 06/24/2019
ms.topic: reference
f1_keywords:
  - "AvoidUnusedParameters"
  - "CA1801"
  - "ReviewUnusedParameters"
helpviewer_keywords:
  - "CA1801"
  - "ReviewUnusedParameters"
ms.assetid: 5d73545c-e153-4b7c-a7b2-be6bf5aca5be
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1801: Review unused parameters

|||
|-|-|
|TypeName|ReviewUnusedParameters|
|CheckId|CA1801|
|Category|Microsoft.Usage|
|Breaking Change|Non Breaking - If the member is not visible outside the assembly, regardless of the change you make.<br /><br /> Non Breaking - If you change the member to use the parameter within its body.<br /><br /> Breaking - If you remove the parameter and it is visible outside the assembly.|

## Cause

A method signature includes a parameter that's not used in the method body.

This rule does not examine the following kinds of methods:

- Methods referenced by a delegate.

- Methods used as event handlers.

- Methods declared with the `abstract` (`MustOverride` in Visual Basic) modifier.

- Methods declared with the `virtual` (`Overridable` in Visual Basic) modifier.

- Methods declared with the `override` (`Overrides` in Visual Basic) modifier.

- Methods declared with the `extern` (`Declare` statement in Visual Basic) modifier.

If you're using [FxCop analyzers](install-fxcop-analyzers.md), this rule does not flag parameters that are named with the [discard](/dotnet/csharp/discards) symbol, for example, `_`, `_1`, and `_2`. This reduces warning noise on parameters that are needed for signature requirements, for example, a method used as a delegate, a parameter with special attributes, or a parameter whose value is implicitly accessed at run time by a framework but is not referenced in code.

## Rule description

Review parameters in non-virtual methods that are not used in the method body to make sure no incorrectness exists around failure to access them. Unused parameters incur maintenance and performance costs.

Sometimes, a violation of this rule can point to an implementation bug in the method. For example, the parameter should have been used in the method body. Suppress warnings of this rule if the parameter must exist because of backward compatibility.

## How to fix violations

To fix a violation of this rule, remove the unused parameter (a breaking change), or use the parameter in the method body (a non-breaking change).

## When to suppress warnings

It is safe to suppress a warning from this rule:

- In previously shipped code for which the fix would be a breaking change.

- For the `this` parameter in a custom extension method for <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert?displayProperty=nameWithType>. The functions in the <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> class are static, so there's no need to access the `this` parameter in the method body.

## Example

The following example shows two methods. One method violates the rule and the other method satisfies the rule.

[!code-csharp[FxCop.Usage.ReviewUnusedParameters#1](../code-quality/codesnippet/CSharp/ca1801-review-unused-parameters_1.cs)]

## Related rules

[CA1811: Avoid uncalled private code](../code-quality/ca1811-avoid-uncalled-private-code.md)

[CA1812: Avoid uninstantiated internal classes](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

[CA1804: Remove unused locals](../code-quality/ca1804-remove-unused-locals.md)
