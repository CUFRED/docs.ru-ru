---
title: Оператор Like
ms.date: 07/20/2015
f1_keywords:
- Like
- vb.Like
helpviewer_keywords:
- similar to
- pattern matching
- Like operator [Visual Basic]
- '? symbol, wildcard character'
- string comparison [Visual Basic], Like operator
- strings [Visual Basic], comparing
- comparison operators [Visual Basic]
- symbols, wildcard
- wildcards, Like operator
- strings [Visual Basic], matching
- string comparison [Visual Basic], sorting data
- data [Visual Basic], sorting
- text [Visual Basic], comparing
- operators [Visual Basic], pattern-matching
- data [Visual Basic], string comparisons
- string comparison [Visual Basic], Like operators
ms.assetid: 966283ec-80e2-4294-baa8-c75baff804f9
ms.openlocfilehash: 4279d90c74c80403146448a8ba5a6051ec9d12f6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401564"
---
# <a name="like-operator-visual-basic"></a>Оператор Like (Visual Basic)
Сравнивает строку с шаблоном.  

> [!IMPORTANT]
> В `Like` настоящее время оператор не поддерживается в проектах .NET Core и .NET Standard.

## <a name="syntax"></a>Синтаксис  
  
```vb  
result = string Like pattern  
```  
  
## <a name="parts"></a>Компоненты  
 `result`  
 Обязательный. Любая `Boolean` переменная. Результатом является `Boolean` значение, указывающее, удовлетворяет ли объект `string` `pattern` .  
  
 `string`  
 Обязательный. Произвольное выражение `String` .  
  
 `pattern`  
 Обязательный. Любое `String` выражение, удовлетворяющее соглашениям о соответствии шаблону, описанным в разделе «Примечания».  
  
## <a name="remarks"></a>Комментарии  
 Если значение в параметре `string` соответствует шаблону, содержащемуся в `pattern` , `result` то является `True` . Если строка не соответствует шаблону, `result` то параметр имеет значение `False` . Если `string` и, и `pattern` являются пустыми строками, результатом будет `True` .  
  
## <a name="comparison-method"></a>Метод сравнения  
 Поведение `Like` оператора зависит от [оператора Option Compare](../statements/option-compare-statement.md). По умолчанию для каждого исходного файла используется метод сравнения строк `Option Compare Binary` .  
  
## <a name="pattern-options"></a>Параметры шаблона  
 Встроенное сопоставление шаблонов предоставляет универсальное средство для сравнения строк. Функции сопоставления шаблонов позволяют сопоставлять каждый символ с `string` конкретным символом, подстановочным знаком, списком символов или диапазоном символов. В следующей таблице приведены символы, разрешенные в `pattern` , и их соответствие.  
  
|Символы в`pattern`|Соответствия в`string`|  
|-----------------------------|-------------------------|  
|`?`|Любой отдельный символ|  
|`*`|Ноль или более символов|  
|`#`|Любая отдельная цифра (0 – 9)|  
|`[charlist]`|Любой отдельный символ в`charlist`|  
|`[!charlist]`|Любой отдельный символ, не являющийся`charlist`|  
  
## <a name="character-lists"></a>Списки символов  
 Группа из одного или нескольких символов ( `charlist` ), заключенных в квадратные скобки ( `[ ]` ), может использоваться для сопоставления любого отдельного символа в `string` и может включать практически любой код символа, включая цифры.  
  
 Восклицательный знак ( `!` ) в начале `charlist` означает, что сопоставление выполняется, если какой-либо символ, кроме символов в `charlist` , находится в `string` . При использовании вне квадратных скобок восклицательный знак соответствует самому себе.  
  
## <a name="special-characters"></a>Специальные символы  
 Чтобы сопоставить специальные символы с левой скобкой ( `[` ), вопросительный знак ( `?` ), знак решетки ( `#` ) и звездочка ( `*` ), заключите их в квадратные скобки. Правая квадратная скобка ( `]` ) не может использоваться в группе для сопоставления самой себе, но ее можно использовать за пределами группы в качестве отдельного символа.  
  
 Последовательность символов `[]` считается строкой нулевой длины ( `""` ). Однако она не может входить в список символов, заключенный в квадратные скобки. Если вы хотите проверить, является ли элемент в какой `string` -либо из групп символов или вообще не содержать ни одного символа, можно использовать `Like` дважды. Пример см. в разделе [как сопоставить строку с шаблоном](../../programming-guide/language-features/operators-and-expressions/how-to-match-a-string-against-a-pattern.md).  
  
## <a name="character-ranges"></a>Диапазоны символов  
 Используя дефис ( `–` ) для разделения нижней и верхней границ диапазона, `charlist` можно указать диапазон символов. Например, `[A–Z]` результатом является совпадение, если соответствующая символьная позиции в `string` содержит любой символ в диапазоне `A` — `Z` , и `[!H–L]` результатом является совпадение, если соответствующая символьная позиции содержит любой символ за пределами диапазона `H` — `L` .  
  
 При указании диапазона символов они должны отображаться в порядке сортировки по возрастанию, то есть от самого низкого до самого высокого. Таким образом, `[A–Z]` является допустимым шаблоном, но `[Z–A]` не является.  
  
### <a name="multiple-character-ranges"></a>Несколько диапазонов символов  
 Чтобы указать несколько диапазонов для одной позиции символа, поместите их в одни и те же квадратные скобки без разделителей. Например, `[A–CX–Z]` результатом является совпадение, если соответствующая символьная позиции в `string` содержит любой символ либо в диапазоне `A` , `C` либо в диапазоне `X` — `Z` .  
  
### <a name="usage-of-the-hyphen"></a>Использование дефиса  
 Дефис ( `–` ) может располагаться в начале (после восклицательного знака, если есть) или в конце, `charlist` чтобы соответствовать самому себе. В любом другом расположении дефис определяет диапазон символов, разделенных символами с любой стороны дефиса.  
  
## <a name="collating-sequence"></a>Порядок сортировки  
 Значение указанного диапазона зависит от порядка символов во время выполнения, определенного `Option Compare` параметром, и параметра языкового стандарта системы, в которой выполняется код. В параметр `Option Compare Binary` Range соответствует значениям `[A–E]` `A` , `B` ,, `C` `D` и `E` . С `Option Compare Text` , `[A–E]` соответствует `A` , `a` ,,, `À` `à` `B` , `b` , `C` , `c` , `D` , `d` , `E` и `e` . Диапазон не совпадает `Ê` , или, `ê` так как диакритические знаки сортируются после символов без диакритических знаков в порядке сортировки.  
  
## <a name="digraph-characters"></a>Символы раскрутки  
 В некоторых языках есть алфавитные символы, представляющие два отдельных символа. Например, несколько языков используют символ `æ` для представления символов `a` и, `e` когда они появляются вместе. `Like`Оператор распознает, что один и тот же символ раскрутки и два отдельных символа эквивалентны.  
  
 Если в настройках языкового стандарта системы задан язык, использующий символ относительных значений, то вхождение одного символа относительных значений в `pattern` или `string` соответствует последовательности двух символов в другой строке. Аналогично, символ отсчета в `pattern` квадратных скобках (сам по себе, в списке или в диапазоне) совпадает с эквивалентной последовательностью двух символов в `string` .  
  
## <a name="overloading"></a>Перегрузка  
 `Like`Оператор можно *перегрузить*, что означает, что класс или структура может переопределить свое поведение, когда операнд имеет тип этого класса или структуры. Если код использует этот оператор для такого класса или структуры, убедитесь, что вы понимаете его переопределенное поведение. Для получения дополнительной информации см. [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Пример  
 В этом примере `Like` оператор используется для сравнения строк с различными шаблонами. Результаты попадают в `Boolean` переменную, указывающую, соответствует ли каждая строка шаблону.  
  
 [!code-vb[VbVbalrOperators#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#30)]  
  
## <a name="see-also"></a>См. также раздел

- <xref:Microsoft.VisualBasic.Strings.InStr%2A>
- <xref:Microsoft.VisualBasic.Strings.StrComp%2A>
- [Операторы сравнения](comparison-operators.md)
- [Порядок применения операторов в Visual Basic](operator-precedence.md)
- [Список операторов, сгруппированных по функциональному назначению](operators-listed-by-functionality.md)
- [Оператор Option Compare](../statements/option-compare-statement.md)
- [Операторы и выражения](../../programming-guide/language-features/operators-and-expressions/index.md)
- [Практическое руководство. Сравнение строки на соответствие с шаблоном](../../programming-guide/language-features/operators-and-expressions/how-to-match-a-string-against-a-pattern.md)
