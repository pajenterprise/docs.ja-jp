---
title: '方法: Parallel.For または ForEach ループを取り消す'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel foreach loop, how to cancel
- parallel for loops, how to cancel
ms.assetid: 9d19b591-ea95-4418-8ea7-b6266af9905b
ms.openlocfilehash: d29137127dd47844f8f08d3ac689cf2827d9efe2
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288226"
---
# <a name="how-to-cancel-a-parallelfor-or-foreach-loop"></a>方法: Parallel.For または ForEach ループを取り消す
<xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> および <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> メソッドでは、キャンセル トークンを使用した取り消し処理がサポートされます。 一般的な取り消し処理の詳細については、「[キャンセル](../threading/cancellation-in-managed-threads.md)」を参照してください。 並列ループでは、<xref:System.Threading.Tasks.ParallelOptions> パラメーターのメソッドに <xref:System.Threading.CancellationToken> を指定してから、try-catch ブロックで並列呼び出しを囲みます。  
  
## <a name="example"></a>例  
 次の例は、<xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> の呼び出しを取り消す方法を示しています。 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 呼び出しに同じ方法を適用できます。  
  
 [!code-csharp[TPL_Parallel#29](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/parallel_cancel.cs#29)]
 [!code-vb[TPL_Parallel#29](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/cancelloop.vb#29)]  
  
 取り消しを通知するトークンが <xref:System.Threading.Tasks.ParallelOptions> インスタンスで指定されているのと同じトークンである場合、並列ループは取り消し時に単一の <xref:System.OperationCanceledException> をスローします。 その他のいくつかのトークンによって取り消しが行われた場合、ループは InnerException として <xref:System.OperationCanceledException> と共に <xref:System.AggregateException> をスローします。  
  
## <a name="see-also"></a>参照

- [データの並列化](data-parallelism-task-parallel-library.md)
- [PLINQ および TPL のラムダ式](lambda-expressions-in-plinq-and-tpl.md)
