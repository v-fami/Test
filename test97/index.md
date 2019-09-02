---
title: 无法根据这些自变量推断出方法 "<methodname>" 中类型参数的数据类型, 因为可能存在多个类型
ms.date: 07/20/2015
f1_keywords:
- bc36651
- bc36654
- vbc36651
- vbc36654
helpviewer_keywords:
- BC36651
- BC36654
ms.assetid: d4bf408c-ca1f-44ad-855a-3df898de60c6
ms.openlocfilehash: c0818d31bcc3b8ecfda42dac89496d58a339afce
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "68631070"
---
# <a name="data-types-of-the-type-parameters-in-method-methodname-cannot-be-inferred-from-these-arguments-because-more-than-one-type-is-possible"></a>无法根据这些自变量推断出方法 "\<>" 中类型参数的数据类型, 因为可能存在多个类型

无法根据这些自变量推断出方法 "\<方法名称 >" 中类型参数的数据类型, 因为可能有多种类型。 显式指定数据类型可更正此错误。

尝试使用类型推理功能在对泛型过程的调用中确定类型参数或参数的类型。 编译器发现一个或多个类型参数的多个可能的数据类型，并报告此错误。

> [!NOTE]
> 当无法指定实参时（例如，对于查询表达式中的查询运算符），显示的错误消息不包括第二个句子。

下面的代码演示了此错误。

```vb
Option Strict Off
Module Module1
    Sub Main()
        '' Not valid.
        'targetMethod(1, "2")
    End Sub

    Sub targetMethod(Of T)(ByVal p1 As T, ByVal p2 As T)
    End Sub

End Module
```

**错误 ID:** BC36654 (在[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]查询中) 和 BC36651 (在查询外)

## <a name="to-correct-this-error"></a>更正此错误

如果此错误出现在查询外，请尝试显式指定类型参数的数据类型：

```vb
targetMethod(Of Integer)(1, "2")
```

## <a name="see-also"></a>请参阅

- [Option Strict 语句](../../visual-basic/language-reference/statements/option-strict-statement.md)
- [Generic Procedures in Visual Basic](../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md)
