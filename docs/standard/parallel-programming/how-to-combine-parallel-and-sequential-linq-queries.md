---
title: Практическое руководство. Объединение параллельных и последовательных запросов LINQ
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel queries, combine parallel and sequential
ms.assetid: 1167cfe6-c8aa-4096-94ba-c66c3a4edf4c
ms.openlocfilehash: 2bdf074bc2977dc501e0726a52e825c89828565f
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289542"
---
# <a name="how-to-combine-parallel-and-sequential-linq-queries"></a>Практическое руководство. Объединение параллельных и последовательных запросов LINQ

Этот пример демонстрирует применение метода <xref:System.Linq.ParallelEnumerable.AsSequential%2A>, который запрашивает последовательную обработку в PLINQ всех последующих операторов текущего запроса. Обычно последовательная обработка выполняется медленнее, чем параллельная, но иногда она необходима, чтобы гарантировать правильные результаты.  
  
> [!NOTE]
> Этот пример предназначен для демонстрации использования и может выполняться не быстрее аналогичного последовательного запроса LINQ to Objects. См. дополнительные сведения об [ускорении выполнения в PLINQ](understanding-speedup-in-plinq.md).  
  
## <a name="example"></a>Пример  
 Следующий пример демонстрирует одну из ситуаций, для которой необходимо <xref:System.Linq.ParallelEnumerable.AsSequential%2A>, поскольку здесь важно сохранить порядок, установленный предыдущим предложением запроса.  
  
 [!code-csharp[PLINQ#24](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#24)]
 [!code-vb[PLINQ#24](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#24)]  
  
## <a name="compiling-the-code"></a>Компиляция кода  
 Чтобы скомпилировать и запустить этот код, вставьте его в проект [Пример данных PLINQ](plinq-data-sample.md), добавьте строку с вызовом этого метода из `Main` и нажмите клавишу **F5**.  
  
## <a name="see-also"></a>См. также

- [Parallel LINQ (PLINQ)](introduction-to-plinq.md)
