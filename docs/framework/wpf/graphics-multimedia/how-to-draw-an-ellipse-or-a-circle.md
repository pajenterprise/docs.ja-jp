---
title: '方法: 楕円または円を描画する'
ms.date: 03/30/2017
helpviewer_keywords:
- ellipses [WPF], drawing
- circles [WPF], drawing
- drawing circles [WPF]
- drawing ellipses [WPF]
- graphics [WPF], drawing circles
- graphics [WPF], drawing ellipses
ms.assetid: 99763b8c-bfc8-44be-8231-8a70daf5481a
ms.openlocfilehash: 5f17615da4907cba6e25b68f2f934602c2f8a390
ms.sourcegitcommit: 700ea803fb06c5ce98de017c7f76463ba33ff4a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77452923"
---
# <a name="how-to-draw-an-ellipse-or-a-circle"></a>方法: 楕円または円を描画する
この例では、<xref:System.Windows.Shapes.Ellipse> 要素を使用して、楕円と円を描画する方法を示します。 楕円を描画するには、<xref:System.Windows.Shapes.Ellipse> 要素を作成し、その <xref:System.Windows.FrameworkElement.Width%2A> と <xref:System.Windows.FrameworkElement.Height%2A>を指定します。 <xref:System.Windows.Shapes.Shape.Fill%2A> プロパティを使用して、楕円の内部を描画するために使用される <xref:System.Windows.Media.Brush> を指定します。 <xref:System.Windows.Shapes.Shape.Stroke%2A> プロパティを使用して、楕円の輪郭の描画に使用される <xref:System.Windows.Media.Brush> を指定します。 <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> プロパティは、楕円の輪郭の太さを指定します。  
  
 円を描画するには、<xref:System.Windows.Shapes.Ellipse> 要素の <xref:System.Windows.FrameworkElement.Width%2A> と <xref:System.Windows.FrameworkElement.Height%2A> が等しくなるようにします。  
  
 次の例では、<xref:System.Windows.Controls.Canvas> 内に 4 つの <xref:System.Windows.Shapes.Ellipse> 要素を描画しています。  
  
## <a name="example"></a>例  
 [!code-xaml[drawingwithshapeelements#EllipseExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/ellipseexample.xaml#ellipseexample1)]  
  
 この例では、<xref:System.Windows.Controls.Canvas> を使用して楕円を格納していますが、テキスト以外のコンテンツをサポートする <xref:System.Windows.Controls.Panel> または <xref:System.Windows.Controls.Control> で楕円要素 (およびその他のすべての図形要素) を使用できます。  
  
 この例は、より大きなサンプルの一部です。サンプル全体については、「[Shape 要素のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ShapeElements)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Shapes.Ellipse>
- <xref:System.Windows.Shapes.Shape>
- [Shape 要素のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ShapeElements)
