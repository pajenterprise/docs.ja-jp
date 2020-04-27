---
title: XamlName の文法
ms.date: 03/30/2017
helpviewer_keywords:
- DottedXamlName grammar [XAML Services]
- grammar [XAML Services], DottedXamlName
- grammar [XAML Services], XamlName
- names in XAML [XAML Services]
- XamlName grammar [XAML Services]
ms.assetid: 11e4cada-41d2-494d-9531-0d3df4dfcbe3
ms.openlocfilehash: 2fc74990b15caaa9b58e6eea5b0212ea22505674
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "81433050"
---
# <a name="xamlname-grammar"></a><span data-ttu-id="6f5fe-102">XamlName の文法</span><span class="sxs-lookup"><span data-stu-id="6f5fe-102">XamlName Grammar</span></span>

<span data-ttu-id="6f5fe-103">XamlName 文法は、XAML 言語仕様 [MS-XAML] で定義されている特定の文法です。</span><span class="sxs-lookup"><span data-stu-id="6f5fe-103">XamlName Grammar is a specific grammar that is defined in the XAML language specification [MS-XAML], which is reproduced here for convenience.</span></span>

## <a name="from-the-xaml-specification"></a><span data-ttu-id="6f5fe-104">XAML 仕様から</span><span class="sxs-lookup"><span data-stu-id="6f5fe-104">From the XAML Specification</span></span>

<span data-ttu-id="6f5fe-105">[MS-XAML] 仕様では、型とプロパティに使用される一連の有効なシンボル識別子を識別する文法 XamlName が定義されています。</span><span class="sxs-lookup"><span data-stu-id="6f5fe-105">The [MS-XAML] specification defines the grammar XamlName to identify the set of legal symbolic identifiers used for types and properties.</span></span>

<span data-ttu-id="6f5fe-106">XamlName 型の文字列値は、次の文法に準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f5fe-106">String values that are of type XamlName must conform to the following grammar:</span></span>

```xaml
XamlName ::= NameStartChar ( NameChar )*
NameStartChar ::= LetterCharacter | '_'
NameChar ::= NameStartChar | DecimalDigit | CombiningCharacter
LetterCharacter ::= UnicodeLu | UnicodeLl | UnicodeLo | UnicodeLt | UnicodeNl
DecimalDigit ::= UnicodeNd
CombiningCharacter ::= UnicodeMn | UnicodeMc
```

<span data-ttu-id="6f5fe-107">Unicode 文字データベースで定義されている次の一般的なカテゴリ値を想定しています。</span><span class="sxs-lookup"><span data-stu-id="6f5fe-107">Which assumes the following general category values as defined in the Unicode Character Database</span></span>

| <span data-ttu-id="6f5fe-108">ユニコードカテゴリ</span><span class="sxs-lookup"><span data-stu-id="6f5fe-108">Unicode category</span></span>   | <span data-ttu-id="6f5fe-109">説明</span><span class="sxs-lookup"><span data-stu-id="6f5fe-109">Description</span></span>                   |
|--------------------|-------------------------------|
| <span data-ttu-id="6f5fe-110">ルー語</span><span class="sxs-lookup"><span data-stu-id="6f5fe-110">Lu</span></span>                 | <span data-ttu-id="6f5fe-111">Letter, Uppercase (字、大文字)</span><span class="sxs-lookup"><span data-stu-id="6f5fe-111">Letter, Uppercase</span></span>             |
| <span data-ttu-id="6f5fe-112">Ll</span><span class="sxs-lookup"><span data-stu-id="6f5fe-112">Ll</span></span>                 | <span data-ttu-id="6f5fe-113">Letter, Lowercase (字、小文字)</span><span class="sxs-lookup"><span data-stu-id="6f5fe-113">Letter, Lowercase</span></span>             |
| <span data-ttu-id="6f5fe-114">Lt</span><span class="sxs-lookup"><span data-stu-id="6f5fe-114">Lt</span></span>                 | <span data-ttu-id="6f5fe-115">Letter, Titlecase (字、タイトル文字)</span><span class="sxs-lookup"><span data-stu-id="6f5fe-115">Letter, Titlecase</span></span>             |
| <span data-ttu-id="6f5fe-116">Lm</span><span class="sxs-lookup"><span data-stu-id="6f5fe-116">Lm</span></span>                 | <span data-ttu-id="6f5fe-117">Letter, Modifier (字、修飾)</span><span class="sxs-lookup"><span data-stu-id="6f5fe-117">Letter, Modifier</span></span>              |
| <span data-ttu-id="6f5fe-118">Lo</span><span class="sxs-lookup"><span data-stu-id="6f5fe-118">Lo</span></span>                 | <span data-ttu-id="6f5fe-119">Letter, Other (字、その他)</span><span class="sxs-lookup"><span data-stu-id="6f5fe-119">Letter, Other</span></span>                 |
| <span data-ttu-id="6f5fe-120">Mn</span><span class="sxs-lookup"><span data-stu-id="6f5fe-120">Mn</span></span>                 | <span data-ttu-id="6f5fe-121">マーク、非間隔</span><span class="sxs-lookup"><span data-stu-id="6f5fe-121">Mark, Non-Spacing</span></span>             |
| <span data-ttu-id="6f5fe-122">Mc</span><span class="sxs-lookup"><span data-stu-id="6f5fe-122">Mc</span></span>                 | <span data-ttu-id="6f5fe-123">Mark, Spacing Combining (結合文字、幅あり)</span><span class="sxs-lookup"><span data-stu-id="6f5fe-123">Mark, Spacing Combining</span></span>       |
| <span data-ttu-id="6f5fe-124">Nd</span><span class="sxs-lookup"><span data-stu-id="6f5fe-124">Nd</span></span>                 | <span data-ttu-id="6f5fe-125">数値、小数</span><span class="sxs-lookup"><span data-stu-id="6f5fe-125">Number, Decimal</span></span>               |
| <span data-ttu-id="6f5fe-126">Nl</span><span class="sxs-lookup"><span data-stu-id="6f5fe-126">Nl</span></span>                 | <span data-ttu-id="6f5fe-127">Number, Letter (数、字)</span><span class="sxs-lookup"><span data-stu-id="6f5fe-127">Number, Letter</span></span>                |

<span data-ttu-id="6f5fe-128">XAML では、プロパティとイベント修飾参照、およびアタッチされたメンバーに対して使用される 2 番目の文法 DXamlName を定義します。</span><span class="sxs-lookup"><span data-stu-id="6f5fe-128">XAML defines a second grammar, DottedXamlName, that is used for property and event qualified references, and also for attached members.</span></span> <span data-ttu-id="6f5fe-129">詳細については、「 と<xref:System.Windows.DependencyProperty> [XAML の概要 (WPF)](../fundamentals/xaml.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6f5fe-129">For more information, see <xref:System.Windows.DependencyProperty> and [XAML Overview (WPF)](../fundamentals/xaml.md).</span></span>

<span data-ttu-id="6f5fe-130">型が DXamlName の文字列値は、次の文法に準拠する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f5fe-130">String values that are of type DottedXamlName must conform to the following grammar:</span></span>

```xaml
DottedXamlName ::= XamlName '.' XamlName
```

## <a name="remarks"></a><span data-ttu-id="6f5fe-131">解説</span><span class="sxs-lookup"><span data-stu-id="6f5fe-131">Remarks</span></span>

<span data-ttu-id="6f5fe-132">完全な仕様については、 [ \[MS-XAML\]](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6f5fe-132">For the complete specification, see [\[MS-XAML\]](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10)).</span></span>