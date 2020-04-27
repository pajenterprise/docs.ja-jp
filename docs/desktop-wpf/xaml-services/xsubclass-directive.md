---
title: x:Subclass ディレクティブ
ms.date: 03/30/2017
f1_keywords:
- Subclass
- xSubclass
- x:Subclass
helpviewer_keywords:
- x:Subclass attribute [XAML Services]
- XAML [XAML Services], x:Subclass attribute
- Subclass attribute in XAML [XAML Services]
ms.assetid: 99f66072-8107-4362-ab99-8171dc83b469
ms.openlocfilehash: e85e0fb5a0e1a865ed84a93767f8152a115bbe5f
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432642"
---
# <a name="xsubclass-directive"></a><span data-ttu-id="74838-102">x:Subclass ディレクティブ</span><span class="sxs-lookup"><span data-stu-id="74838-102">x:Subclass Directive</span></span>

<span data-ttu-id="74838-103">XAML マークアップ コンパイル動作を`x:Class`変更します ( 指定されている場合 ) 。</span><span class="sxs-lookup"><span data-stu-id="74838-103">Modifies XAML markup compile behavior when `x:Class` is also provided.</span></span> <span data-ttu-id="74838-104">に`x:Class`基づく部分クラスを作成する代わりに、提供`x:Class`されるクラスは中間クラスとして作成され、指定された派生クラスは に基`x:Class`づくと想定されます。</span><span class="sxs-lookup"><span data-stu-id="74838-104">Instead of creating a partial class that is based on `x:Class`, the provided `x:Class` is created as an intermediate class, and then your provided derived class is expected to be based on `x:Class`.</span></span>

## <a name="xaml-attribute-usage"></a><span data-ttu-id="74838-105">XAML 属性の使用方法</span><span class="sxs-lookup"><span data-stu-id="74838-105">XAML Attribute Usage</span></span>

```xaml
<object x:Class="namespace.classname" x:Subclass="subclassNamespace.subclassName">
   ...
</object>
```

## <a name="xaml-values"></a><span data-ttu-id="74838-106">XAML 値</span><span class="sxs-lookup"><span data-stu-id="74838-106">XAML Values</span></span>

|||
|-|-|
|`namespace`|<span data-ttu-id="74838-107">省略可能。</span><span class="sxs-lookup"><span data-stu-id="74838-107">Optional.</span></span> <span data-ttu-id="74838-108">を含む`classname`CLR 名前空間を指定します。</span><span class="sxs-lookup"><span data-stu-id="74838-108">Specifies a CLR namespace that contains `classname`.</span></span> <span data-ttu-id="74838-109">指定`namespace`した場合、ドット (.) は`namespace`、`classname`と を区切ります。</span><span class="sxs-lookup"><span data-stu-id="74838-109">If `namespace` is specified, a dot (.) separates `namespace` and `classname`.</span></span>|
|`classname`|<span data-ttu-id="74838-110">必須。</span><span class="sxs-lookup"><span data-stu-id="74838-110">Required.</span></span> <span data-ttu-id="74838-111">読み込まれた XAML とその XAML の分離コードを接続する部分クラスの CLR 名を指定します。</span><span class="sxs-lookup"><span data-stu-id="74838-111">Specifies the CLR name of the partial class that connects the loaded XAML and your code-behind for that XAML.</span></span> <span data-ttu-id="74838-112">「解説」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="74838-112">See Remarks.</span></span>|
|`subclassNamespace`|<span data-ttu-id="74838-113">省略可能。</span><span class="sxs-lookup"><span data-stu-id="74838-113">Optional.</span></span> <span data-ttu-id="74838-114">各名前空間が他`namespace`の名前空間を解決できる場合とは異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="74838-114">Can be different from `namespace` if each namespace can resolve the other.</span></span> <span data-ttu-id="74838-115">を含む`subclassName`CLR 名前空間を指定します。</span><span class="sxs-lookup"><span data-stu-id="74838-115">Specifies a CLR namespace that contains `subclassName`.</span></span> <span data-ttu-id="74838-116">指定`subclassName`した場合、ドット (.) は`subclassNamespace`、`subclassName`と を区切ります。</span><span class="sxs-lookup"><span data-stu-id="74838-116">If `subclassName` is specified, a dot (.) separates `subclassNamespace` and `subclassName`.</span></span>|
|`subclassName`|<span data-ttu-id="74838-117">必須。</span><span class="sxs-lookup"><span data-stu-id="74838-117">Required.</span></span> <span data-ttu-id="74838-118">サブクラスの CLR 名を指定します。</span><span class="sxs-lookup"><span data-stu-id="74838-118">Specifies the CLR name of the subclass.</span></span>|

## <a name="dependencies"></a><span data-ttu-id="74838-119">依存関係</span><span class="sxs-lookup"><span data-stu-id="74838-119">Dependencies</span></span>

<span data-ttu-id="74838-120">[x: Class ディレクティブ](xclass-directive.md)も同じオブジェクトに提供する必要があり、そのオブジェクトは XAML 運用環境のルート要素である必要があります。</span><span class="sxs-lookup"><span data-stu-id="74838-120">[x:Class Directive](xclass-directive.md) must also be provided on the same object, and that object must be the root element of the XAML production.</span></span>

## <a name="remarks"></a><span data-ttu-id="74838-121">解説</span><span class="sxs-lookup"><span data-stu-id="74838-121">Remarks</span></span>

<span data-ttu-id="74838-122">`x:Subclass`使用法は、主に部分クラス宣言をサポートしない言語を対象としています。</span><span class="sxs-lookup"><span data-stu-id="74838-122">`x:Subclass` usage is primarily intended for languages that do not support partial class declarations.</span></span>

<span data-ttu-id="74838-123">として`x:Subclass`使用されるクラスは、入れ子になったクラスにすることはできません`x:Subclass`。</span><span class="sxs-lookup"><span data-stu-id="74838-123">The class used as the `x:Subclass` cannot be a nested class, and `x:Subclass` must refer to the root object as explained in the "Dependencies" section.</span></span>

<span data-ttu-id="74838-124">それ以外の場合、概`x:Subclass`念的な意味は .NET XAML サービスの実装によって定義されていません。</span><span class="sxs-lookup"><span data-stu-id="74838-124">Otherwise, the conceptual meaning of `x:Subclass` is undefined by a .NET XAML Services implementation.</span></span> <span data-ttu-id="74838-125">これは、.NET XAML サービスの動作では、XAML マークアップとバッキング コードが接続される全体的なプログラミング モデルが指定されないためです。</span><span class="sxs-lookup"><span data-stu-id="74838-125">This is because .NET XAML Services behavior does not specify the overall programming model by which XAML markup and backing code are connected.</span></span> <span data-ttu-id="74838-126">プログラミング モデルまたはアプリケーション モデル`x:Class`を`x:Subclass`使用して、XAML マークアップ、コンパイル済みマークアップ、および CLR ベースの分離コードを接続する方法を定義する特定のフレームワークによって、さらに概念の実装が実行されます。</span><span class="sxs-lookup"><span data-stu-id="74838-126">Implementations of further concepts related to `x:Class` and `x:Subclass` are performed by specific frameworks that use programming models or application models to define how to connect XAML markup, compiled markup, and CLR-based code-behind.</span></span> <span data-ttu-id="74838-127">各フレームワークには、動作の一部を有効にする独自のビルド アクション、またはビルド環境に含める必要がある特定のコンポーネントを持つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="74838-127">Each framework might have its own build actions that enable some of the behavior, or specific components that must be included in the build environment.</span></span> <span data-ttu-id="74838-128">フレームワーク内では、ビルド アクションは分離コードに使用される特定の CLR 言語によって異なる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="74838-128">Within a framework, build actions can also vary based on the specific CLR language that is used for the code-behind.</span></span>

## <a name="wpf-usage-notes"></a><span data-ttu-id="74838-129">WPF の使用上の注意</span><span class="sxs-lookup"><span data-stu-id="74838-129">WPF Usage Notes</span></span>

<span data-ttu-id="74838-130">`x:Subclass`ページ ルートまたはアプリケーション定義の<xref:System.Windows.Application>ルートに指定できます。 `x:Class`</span><span class="sxs-lookup"><span data-stu-id="74838-130">`x:Subclass` can be on a page root or on the <xref:System.Windows.Application> root in the application definition, which already has `x:Class`.</span></span> <span data-ttu-id="74838-131">ページ`x:Subclass`またはアプリケーション ルート以外の要素で宣言するか、存在しない`x:Class`場所で指定すると、コンパイル エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="74838-131">Declaring `x:Subclass` on any element other than a page or application root, or specifying it where no `x:Class` exists, causes a compile-time error.</span></span>

<span data-ttu-id="74838-132">シナリオに対して正しく機能する`x:Subclass`派生クラスの作成は、非常に複雑です。</span><span class="sxs-lookup"><span data-stu-id="74838-132">Creating derived classes that work correctly for the `x:Subclass` scenario is fairly complex.</span></span> <span data-ttu-id="74838-133">中間ファイル (マークアップ コンパイルによってプロジェクトの obj フォルダーに作成される .g ファイルと、.xaml ファイル名を組み込んだ名前) を調べる必要があります。</span><span class="sxs-lookup"><span data-stu-id="74838-133">You might need to examine the intermediate files (the .g files produced in the obj folder of your project by markup compile, with names that incorporate the .xaml file names).</span></span> <span data-ttu-id="74838-134">これらの中間ファイルは、コンパイル済みアプリケーションの結合部分クラス内の特定のプログラミング構成要素の起点を判別するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="74838-134">These intermediate files can help you determine the origin of certain programming constructs in the joined partial classes in the compiled application.</span></span>

<span data-ttu-id="74838-135">コンパイル時に中間クラスで作成された`internal override`ハンドラー`Friend Overrides`のスタブをオーバーライドするには、派生クラスのイベント ハンドラーが ( Microsoft Visual Basic で ) 必要があります。</span><span class="sxs-lookup"><span data-stu-id="74838-135">Event handlers in the derived class must be `internal override` (`Friend Overrides` in Microsoft Visual Basic) in order to override the stubs for the handlers as created in the intermediate class during compilation.</span></span> <span data-ttu-id="74838-136">それ以外の場合、派生クラスの実装は、中間クラスの実装と中間クラス ハンドラーを非表示 (シャドウ) にします。</span><span class="sxs-lookup"><span data-stu-id="74838-136">Otherwise, the derived class implementations hide (shadow) the intermediate class implementation and the intermediate class handlers are not invoked.</span></span>

<span data-ttu-id="74838-137">と の`x:Class``x:Subclass`両方を定義する場合は、 で`x:Class`参照されるクラスの実装を提供する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="74838-137">When you define both `x:Class` and `x:Subclass`, you do not need to provide any implementation for the class that is referenced by `x:Class`.</span></span> <span data-ttu-id="74838-138">コンパイラが中間ファイルで作成するクラスに対`x:Class`して何らかのガイダンスを持つため、属性を使用して名前を付けるだけで済みます (この場合、コンパイラは既定の名前を選択しません)。</span><span class="sxs-lookup"><span data-stu-id="74838-138">You only need to give it a name via the `x:Class` attribute so that the compiler has some guidance for the class that it creates in the intermediate files (the compiler does not select a default name in this case).</span></span> <span data-ttu-id="74838-139">クラスに実装を`x:Class`与えることができます。ただし、これは、 と の`x:Class``x:Subclass`両方を使用する一般的なシナリオではありません。</span><span class="sxs-lookup"><span data-stu-id="74838-139">You can give the `x:Class` class an implementation; however, this is not the typical scenario for using both `x:Class` and `x:Subclass`.</span></span>

## <a name="see-also"></a><span data-ttu-id="74838-140">関連項目</span><span class="sxs-lookup"><span data-stu-id="74838-140">See also</span></span>

- [<span data-ttu-id="74838-141">x:Class ディレクティブ</span><span class="sxs-lookup"><span data-stu-id="74838-141">x:Class Directive</span></span>](xclass-directive.md)
- [<span data-ttu-id="74838-142">WPF における XAML とカスタム クラス</span><span class="sxs-lookup"><span data-stu-id="74838-142">XAML and Custom Classes for WPF</span></span>](../../framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)