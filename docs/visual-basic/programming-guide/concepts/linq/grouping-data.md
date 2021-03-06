---
title: Группировка данных
ms.date: 07/20/2015
ms.assetid: 8f3a0871-6958-4aef-8f6f-493e189fd57d
ms.openlocfilehash: 8996eee748489c596bc5adc32f53b6b39dbfc6ac
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398387"
---
# <a name="grouping-data-visual-basic"></a>Группирование данных (Visual Basic)
Группированием называют операцию объединения данных в группы таким образом, чтобы у элементов в каждой группе был общий атрибут.  
  
 На следующем рисунке показаны результаты операции группирования последовательности символов. Ключ для каждой группы — это символ.  
  
 ![Схема, показывающая операцию группирования LINQ.](./media/grouping-data/linq-group-operation.png)  
  
 Далее перечислены методы стандартных операторов запроса, которые группируют элементы данных.  
  
## <a name="methods"></a>Методы  
  
|Имя метода|Описание:|Синтаксис выражения запроса Visual Basic|Дополнительные сведения|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|GroupBy|Группирует элементы с общим атрибутом. Каждая группа представлена объектом <xref:System.Linq.IGrouping%602>.|`Group … By … Into …`|<xref:System.Linq.Enumerable.GroupBy%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.GroupBy%2A?displayProperty=nameWithType>|  
|ToLookup|Вставляет элементы в <xref:System.Linq.Lookup%602> (словарь "один ко многим") в зависимости от функции выбора ключа.|Неприменимо.|<xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-example"></a>Пример синтаксиса выражения запроса  
 В следующем примере кода предложение `Group By` используется для группирования целых чисел в списке на основании четности.  
  
```vb  
Dim numbers As New System.Collections.Generic.List(Of Integer)(  
     New Integer() {35, 44, 200, 84, 3987, 4, 199, 329, 446, 208})  
  
Dim query = From number In numbers
            Group By Remainder = (number Mod 2) Into Group  
  
Dim sb As New System.Text.StringBuilder()  
For Each group In query  
    sb.AppendLine(If(group.Remainder = 0, vbCrLf & "Even numbers:", vbCrLf & "Odd numbers:"))  
    For Each num In group.Group  
        sb.AppendLine(num)  
    Next  
Next  
  
' Display the results.  
MsgBox(sb.ToString())  
  
' This code produces the following output:  
  
' Odd numbers:  
' 35  
' 3987  
' 199  
' 329  
  
' Even numbers:  
' 44  
' 200  
' 84  
' 4  
' 446  
' 208  
```  
  
## <a name="see-also"></a>См. также раздел

- <xref:System.Linq>
- [Общие сведения о стандартных операторах запроса (Visual Basic)](standard-query-operators-overview.md)
- [Предложение Group By](../../../language-reference/queries/group-by-clause.md)
- [Пошаговое руководство. Группировка файлов по расширению (LINQ) (Visual Basic)](how-to-group-files-by-extension-linq.md)
- [Инструкции. Разбиение файла на несколько файлов с помощью групп (LINQ) (Visual Basic)](how-to-split-a-file-into-many-files-by-using-groups-linq.md)
