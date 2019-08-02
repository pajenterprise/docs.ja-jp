---
title: 演算子のオーバーロード - C# リファレンス
description: C# 演算子をオーバーロードする方法と、どの C# 演算子がオーバーロード可能かについて説明します。
ms.date: 07/05/2019
f1_keywords:
- operator_CSharpKeyword
helpviewer_keywords:
- operator keyword [C#]
- operator overloading [C#]
ms.openlocfilehash: 77f9d37b7f3232bb1f9bad0466916336801572dd
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2019
ms.locfileid: "68512384"
---
# <a name="operator-overloading-c-reference"></a><span data-ttu-id="7cf8f-103">演算子のオーバーロード (C# リファレンス)</span><span class="sxs-lookup"><span data-stu-id="7cf8f-103">Operator overloading (C# reference)</span></span>

<span data-ttu-id="7cf8f-104">ユーザー定義型は定義済みの C# 演算子をオーバーロードできます。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-104">A user-defined type can overload a predefined C# operator.</span></span> <span data-ttu-id="7cf8f-105">つまり、1 つまたは両方のオペランドに該当する型は、演算のカスタム実装を提供できます。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-105">That is, a type can provide the custom implementation of an operation when one or both operands are of that type.</span></span> <span data-ttu-id="7cf8f-106">オーバーロード可能な C# 演算子は、「[オーバーロード可能な演算子](#overloadable-operators)」のセクションで示します。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-106">The [Overloadable operators](#overloadable-operators) section shows which C# operators can be overloaded.</span></span>

<span data-ttu-id="7cf8f-107">演算子の宣言には `operator` キーワードを使用します。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-107">Use the `operator` keyword to declare an operator.</span></span> <span data-ttu-id="7cf8f-108">演算子の宣言では、次の規則を満たす必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-108">An operator declaration must satisfy the following rules:</span></span>

- <span data-ttu-id="7cf8f-109">これには、`public` と `static` 修飾子の両方が含まれています。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-109">It includes both a `public` and a `static` modifier.</span></span>
- <span data-ttu-id="7cf8f-110">単項演算子に指定できるパラメーター数は 1 です。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-110">A unary operator takes one parameter.</span></span> <span data-ttu-id="7cf8f-111">二項演算子に指定できるパラメーター数は 2 です。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-111">A binary operator takes two parameters.</span></span> <span data-ttu-id="7cf8f-112">どちらの場合も、少なくとも 1 つのパラメーターの型が `T` または `T?` でなければなりません。`T` は演算子の宣言が含まれる型です。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-112">In each case, at least one parameter must have type `T` or `T?` where `T` is the type that contains the operator declaration.</span></span>

<span data-ttu-id="7cf8f-113">次の例は、有理数を表す簡略化された構造を定義しています。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-113">The following example defines a simplified structure to represent a rational number.</span></span> <span data-ttu-id="7cf8f-114">構造体がいくつかの[算術演算子](arithmetic-operators.md)をオーバーロードします。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-114">The structure overloads some of the [arithmetic operators](arithmetic-operators.md):</span></span>

[!code-csharp[fraction example](~/samples/csharp/language-reference/operators/OperatorOverloading.cs)]

<span data-ttu-id="7cf8f-115">`int` から `Fraction` への暗黙的な変換を定義することで、前の例を拡張できます。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-115">You could extend the preceding example by defining an implicit conversion from `int` to `Fraction`.</span></span> <span data-ttu-id="7cf8f-116">その場合、オーバーロードされた演算子はこれら 2 つの型の引数をサポートします。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-116">Then, overloaded operators would support arguments of those two types.</span></span> <span data-ttu-id="7cf8f-117">つまり、整数を分数に足し、結果として分数を取得できるようになります。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-117">That is, it would become possible to add an integer to a fraction and obtain a fraction as a result.</span></span>

<span data-ttu-id="7cf8f-118">また、`operator` キーワードを使用してカスタムの型変換を定義することもできます。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-118">You also use the `operator` keyword to define a custom type conversion.</span></span> <span data-ttu-id="7cf8f-119">詳細については、「[User-defined conversion operators](user-defined-conversion-operators.md)」(ユーザー定義の変換演算子) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-119">For more information, see [User-defined conversion operators](user-defined-conversion-operators.md).</span></span>

## <a name="overloadable-operators"></a><span data-ttu-id="7cf8f-120">オーバーロード可能な演算子</span><span class="sxs-lookup"><span data-stu-id="7cf8f-120">Overloadable operators</span></span>

<span data-ttu-id="7cf8f-121">次の表は、C# 演算子のオーバーロード可/不可に関する情報を示します。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-121">The following table provides information about overloadability of C# operators:</span></span>

| <span data-ttu-id="7cf8f-122">演算子</span><span class="sxs-lookup"><span data-stu-id="7cf8f-122">Operators</span></span> | <span data-ttu-id="7cf8f-123">オーバーロード可/不可</span><span class="sxs-lookup"><span data-stu-id="7cf8f-123">Overloadability</span></span> |
| --------- | --------------- |
|<span data-ttu-id="7cf8f-124">[+](arithmetic-operators.md#unary-plus-and-minus-operators)、[-](arithmetic-operators.md#unary-plus-and-minus-operators)、[!](boolean-logical-operators.md#logical-negation-operator-)、[~](bitwise-and-shift-operators.md#bitwise-complement-operator-)、[++](arithmetic-operators.md#increment-operator-)、[--](arithmetic-operators.md#decrement-operator---)、[true](true-false-operators.md)、[false](true-false-operators.md)</span><span class="sxs-lookup"><span data-stu-id="7cf8f-124">[+](arithmetic-operators.md#unary-plus-and-minus-operators), [-](arithmetic-operators.md#unary-plus-and-minus-operators), [!](boolean-logical-operators.md#logical-negation-operator-), [~](bitwise-and-shift-operators.md#bitwise-complement-operator-), [++](arithmetic-operators.md#increment-operator-), [--](arithmetic-operators.md#decrement-operator---), [true](true-false-operators.md), [false](true-false-operators.md)</span></span>|<span data-ttu-id="7cf8f-125">これらの単項演算子はオーバーロードできます。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-125">These unary operators can be overloaded.</span></span>|
|<span data-ttu-id="7cf8f-126">[+](addition-operator.md)、[-](subtraction-operator.md)、[\*](arithmetic-operators.md#multiplication-operator-)、[/](arithmetic-operators.md#division-operator-)、[%](arithmetic-operators.md#remainder-operator-)、[&](boolean-logical-operators.md#logical-and-operator-)、[&#124;](boolean-logical-operators.md#logical-or-operator-)、[^](boolean-logical-operators.md#logical-exclusive-or-operator-)、[\<\<](bitwise-and-shift-operators.md#left-shift-operator-)、[>>](bitwise-and-shift-operators.md#right-shift-operator-)、[==](equality-operators.md#equality-operator-)、[!=](equality-operators.md#inequality-operator-)、[\<](comparison-operators.md#less-than-operator-)、[>](comparison-operators.md#greater-than-operator-)、[\<=](comparison-operators.md#less-than-or-equal-operator-)、[>=](comparison-operators.md#greater-than-or-equal-operator-)</span><span class="sxs-lookup"><span data-stu-id="7cf8f-126">[+](addition-operator.md), [-](subtraction-operator.md), [\*](arithmetic-operators.md#multiplication-operator-), [/](arithmetic-operators.md#division-operator-), [%](arithmetic-operators.md#remainder-operator-), [&](boolean-logical-operators.md#logical-and-operator-), [&#124;](boolean-logical-operators.md#logical-or-operator-), [^](boolean-logical-operators.md#logical-exclusive-or-operator-), [\<\<](bitwise-and-shift-operators.md#left-shift-operator-), [>>](bitwise-and-shift-operators.md#right-shift-operator-), [==](equality-operators.md#equality-operator-), [!=](equality-operators.md#inequality-operator-), [\<](comparison-operators.md#less-than-operator-), [>](comparison-operators.md#greater-than-operator-), [\<=](comparison-operators.md#less-than-or-equal-operator-), [>=](comparison-operators.md#greater-than-or-equal-operator-)</span></span>|<span data-ttu-id="7cf8f-127">これらの 2 項演算子はオーバーロードできます。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-127">These binary operators can be overloaded.</span></span> <span data-ttu-id="7cf8f-128">特定の演算子はペアでオーバーロードする必要があります。詳細については、この表の後にある注を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-128">Certain operators must be overloaded in pairs; for more information, see the note that follows this table.</span></span>|
|<span data-ttu-id="7cf8f-129">[&&](boolean-logical-operators.md#conditional-logical-and-operator-)、[&#124;&#124;](boolean-logical-operators.md#conditional-logical-or-operator-)</span><span class="sxs-lookup"><span data-stu-id="7cf8f-129">[&&](boolean-logical-operators.md#conditional-logical-and-operator-), [&#124;&#124;](boolean-logical-operators.md#conditional-logical-or-operator-)</span></span>|<span data-ttu-id="7cf8f-130">条件付き論理演算子は、オーバーロードできません。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-130">Conditional logical operators cannot be overloaded.</span></span> <span data-ttu-id="7cf8f-131">ただし、オーバーロードされた [`true` および `false` 演算子](true-false-operators.md)を含む型が特定の方法で `&` または <code>&#124;</code> もオーバーロードしている場合は、その型のオペランドに対してそれぞれ `&&` または <code>&#124;&#124;</code> 演算子の評価が可能になります。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-131">However, if a type with the overloaded [`true` and `false` operators](true-false-operators.md) also overloads the `&` or <code>&#124;</code> operator in a certain way, the `&&` or <code>&#124;&#124;</code> operator, respectively, can be evaluated for the operands of that type.</span></span> <span data-ttu-id="7cf8f-132">詳細については、「[C# 言語仕様](~/_csharplang/spec/introduction.md)」の[ユーザー定義型条件論理演算子](~/_csharplang/spec/expressions.md#user-defined-conditional-logical-operators)に関するセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-132">For more information, see the [User-defined conditional logical operators](~/_csharplang/spec/expressions.md#user-defined-conditional-logical-operators) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>|
|[<span data-ttu-id="7cf8f-133">&#91;&#93;</span><span class="sxs-lookup"><span data-stu-id="7cf8f-133">&#91;&#93;</span></span>](member-access-operators.md#indexer-operator-)|<span data-ttu-id="7cf8f-134">要素へのアクセスはオーバーロード可能な演算子とは見なされていませんが、[インデクサー](../../programming-guide/indexers/index.md)を定義することができます。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-134">Element access is not considered an overloadable operator, but you can define an [indexer](../../programming-guide/indexers/index.md).</span></span>|
|[<span data-ttu-id="7cf8f-135">(T)x</span><span class="sxs-lookup"><span data-stu-id="7cf8f-135">(T)x</span></span>](type-testing-and-conversion-operators.md#cast-operator-)|<span data-ttu-id="7cf8f-136">キャスト演算子はオーバーロードできませんが、新しい変換演算子を定義できます。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-136">The cast operator cannot be overloaded, but you can define new conversion operators.</span></span> <span data-ttu-id="7cf8f-137">詳細については、「[User-defined conversion operators](user-defined-conversion-operators.md)」(ユーザー定義の変換演算子) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-137">For more information, see [User-defined conversion operators](user-defined-conversion-operators.md).</span></span>|
|<span data-ttu-id="7cf8f-138">[+=](arithmetic-operators.md#compound-assignment), [-=](arithmetic-operators.md#compound-assignment), [\*=](arithmetic-operators.md#compound-assignment), [/=](arithmetic-operators.md#compound-assignment), [%=](arithmetic-operators.md#compound-assignment), [&=](boolean-logical-operators.md#compound-assignment), [&#124;=](boolean-logical-operators.md#compound-assignment), [^=](boolean-logical-operators.md#compound-assignment), [\<\<=](bitwise-and-shift-operators.md#compound-assignment), [>>=](bitwise-and-shift-operators.md#compound-assignment)</span><span class="sxs-lookup"><span data-stu-id="7cf8f-138">[+=](arithmetic-operators.md#compound-assignment), [-=](arithmetic-operators.md#compound-assignment), [\*=](arithmetic-operators.md#compound-assignment), [/=](arithmetic-operators.md#compound-assignment), [%=](arithmetic-operators.md#compound-assignment), [&=](boolean-logical-operators.md#compound-assignment), [&#124;=](boolean-logical-operators.md#compound-assignment), [^=](boolean-logical-operators.md#compound-assignment), [\<\<=](bitwise-and-shift-operators.md#compound-assignment), [>>=](bitwise-and-shift-operators.md#compound-assignment)</span></span>|<span data-ttu-id="7cf8f-139">複合代入演算子を明示的にオーバーロードすることはできません。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-139">Compound assignment operators cannot be explicitly overloaded.</span></span> <span data-ttu-id="7cf8f-140">ただし、二項演算子をオーバーロードするとき、対応する複合代入演算子がある場合は、それも暗黙的にオーバーロードされます。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-140">However, when you overload a binary operator, the corresponding compound assignment operator, if any, is also implicitly overloaded.</span></span> <span data-ttu-id="7cf8f-141">たとえば、`+=` は、オーバーロード可能な `+` を使用して評価されます。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-141">For example, `+=` is evaluated using `+`, which can be overloaded.</span></span>|
|<span data-ttu-id="7cf8f-142">[=](assignment-operator.md)、[.](member-access-operators.md#member-access-operator-)、[?:](conditional-operator.md)、[??](null-coalescing-operator.md)、[->](pointer-related-operators.md#pointer-member-access-operator--)、[=>](lambda-operator.md)、[f(x)](member-access-operators.md#invocation-operator-)、[as](type-testing-and-conversion-operators.md#as-operator)、[checked](../keywords/checked.md)、[unchecked](../keywords/unchecked.md)、[default](../../programming-guide/statements-expressions-operators/default-value-expressions.md)、[delegate](delegate-operator.md)、[is](type-testing-and-conversion-operators.md#is-operator)、[nameof](nameof.md)、[new](new-operator.md)、[sizeof](sizeof.md)、[stackalloc](stackalloc.md)、[typeof](type-testing-and-conversion-operators.md#typeof-operator)</span><span class="sxs-lookup"><span data-stu-id="7cf8f-142">[=](assignment-operator.md), [.](member-access-operators.md#member-access-operator-), [?:](conditional-operator.md), [??](null-coalescing-operator.md), [->](pointer-related-operators.md#pointer-member-access-operator--), [=>](lambda-operator.md), [f(x)](member-access-operators.md#invocation-operator-), [as](type-testing-and-conversion-operators.md#as-operator), [checked](../keywords/checked.md), [unchecked](../keywords/unchecked.md), [default](../../programming-guide/statements-expressions-operators/default-value-expressions.md), [delegate](delegate-operator.md), [is](type-testing-and-conversion-operators.md#is-operator), [nameof](nameof.md), [new](new-operator.md), [sizeof](sizeof.md), [stackalloc](stackalloc.md), [typeof](type-testing-and-conversion-operators.md#typeof-operator)</span></span>|<span data-ttu-id="7cf8f-143">これらの演算子はオーバーロードできません。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-143">These operators cannot be overloaded.</span></span>|

> [!NOTE]
> <span data-ttu-id="7cf8f-144">比較演算子は、ペアでオーバーロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-144">The comparison operators must be overloaded in pairs.</span></span> <span data-ttu-id="7cf8f-145">つまり、ペアのどちらかの演算子をオーバーロードする場合、もう一方の演算子もオーバーロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-145">That is, if either operator of a pair is overloaded, the other operator must be overloaded as well.</span></span> <span data-ttu-id="7cf8f-146">次のようなペアがこれに該当します。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-146">Such pairs are as follows:</span></span>
>
> - <span data-ttu-id="7cf8f-147">`==` 演算子と `!=` 演算子</span><span class="sxs-lookup"><span data-stu-id="7cf8f-147">`==` and `!=` operators</span></span>
> - <span data-ttu-id="7cf8f-148">`<` 演算子と `>` 演算子</span><span class="sxs-lookup"><span data-stu-id="7cf8f-148">`<` and `>` operators</span></span>
> - <span data-ttu-id="7cf8f-149">`<=` 演算子と `>=` 演算子</span><span class="sxs-lookup"><span data-stu-id="7cf8f-149">`<=` and `>=` operators</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="7cf8f-150">C# 言語仕様</span><span class="sxs-lookup"><span data-stu-id="7cf8f-150">C# language specification</span></span>

<span data-ttu-id="7cf8f-151">詳細については、「[C# 言語仕様](~/_csharplang/spec/introduction.md)」の次のセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="7cf8f-151">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="7cf8f-152">演算子のオーバーロード</span><span class="sxs-lookup"><span data-stu-id="7cf8f-152">Operator overloading</span></span>](~/_csharplang/spec/expressions.md#operator-overloading)
- [<span data-ttu-id="7cf8f-153">演算子</span><span class="sxs-lookup"><span data-stu-id="7cf8f-153">Operators</span></span>](~/_csharplang/spec/classes.md#operators)

## <a name="see-also"></a><span data-ttu-id="7cf8f-154">関連項目</span><span class="sxs-lookup"><span data-stu-id="7cf8f-154">See also</span></span>

- [<span data-ttu-id="7cf8f-155">C# リファレンス</span><span class="sxs-lookup"><span data-stu-id="7cf8f-155">C# reference</span></span>](../index.md)
- [<span data-ttu-id="7cf8f-156">C# 演算子</span><span class="sxs-lookup"><span data-stu-id="7cf8f-156">C# operators</span></span>](index.md)
- [<span data-ttu-id="7cf8f-157">ユーザー定義の変換演算子</span><span class="sxs-lookup"><span data-stu-id="7cf8f-157">User-defined conversion operators</span></span>](user-defined-conversion-operators.md)
- [<span data-ttu-id="7cf8f-158">C# のオーバーロードされた演算子が常に静的である理由</span><span class="sxs-lookup"><span data-stu-id="7cf8f-158">Why are overloaded operators always static in C#?</span></span>](https://blogs.msdn.microsoft.com/ericlippert/2007/05/14/why-are-overloaded-operators-always-static-in-c/)