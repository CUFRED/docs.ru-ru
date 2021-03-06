---
title: Руководство по программированию на C#. Делегаты
description: Делегат в C# — это тип, который представляет ссылки на методы со списком параметров и типом возвращаемого значения. Делегаты используются для передачи методов в качестве аргументов к другим методам.
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, delegates
- delegates [C#]
ms.assetid: 97de039b-c76b-4b9c-a27d-8c1e1c8d93da
ms.openlocfilehash: 2c1be56b67528c17a6cf1d8d8517817ff93b2aa5
ms.sourcegitcommit: 7476c20d2f911a834a00b8a7f5e8926bae6804d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/11/2020
ms.locfileid: "88063642"
---
# <a name="delegates-c-programming-guide"></a>Делегаты (Руководство по программированию на C#)
[Делегат](../../language-reference/builtin-types/reference-types.md) — это тип, который представляет ссылки на методы с определенным списком параметров и типом возвращаемого значения. При создании экземпляра делегата этот экземпляр можно связать с любым методом с совместимой сигнатурой и типом возвращаемого значения. Метод можно вызвать (активировать) с помощью экземпляра делегата.  
  
 Делегаты используются для передачи методов в качестве аргументов к другим методам. Обработчики событий — это ничто иное, как методы, вызываемые с помощью делегатов. При создании пользовательского метода класс (например, элемент управления Windows) может вызывать этот метод при появлении определенного события. В следующем примере показано объявление делегата:  
  
 [!code-csharp[csProgGuideDelegates#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#20)]  
  
 Делегату можно назначить любой метод из любого доступного класса или структуры, соответствующей типу делегата. Этот метод должен быть статическим методом или методом экземпляра. Это позволяет программно изменять вызовы метода, а также включать новый код в существующие классы.  
  
> [!NOTE]
> В контексте перегрузки метода его сигнатура не содержит возвращаемое значение. Однако в контексте делегатов сигнатура метода содержит возвращаемое значение. Другими словами, метод должен иметь тот же возвращаемый тип, что и делегат.  
  
 Благодаря возможности ссылаться на метод как на параметр делегаты идеально подходят для определения методов обратного вызова. Например, ссылка на метод, сравнивающий два объекта, может быть передана в качестве аргумента алгоритму сортировки. Поскольку код сравнения находится в отдельной процедуре, алгоритм сортировки может быть написан более общим способом.  
  
## <a name="delegates-overview"></a>Общие сведения о делегатах  
 Делегаты имеют следующие свойства.  
  
- Делегаты подобны указателям на функции в C++, но являются полностью объектно-ориентированными и, в отличие от указателей C++ на функции-члены, инкапсулируют экземпляр объекта вместе с методом.
  
- Делегаты допускают передачу методов в качестве параметров.  
  
- Делегаты можно использовать для определения методов обратного вызова.  
  
- Делегаты можно связывать друг с другом; например, при появлении одного события можно вызывать несколько методов.  
  
- Точное соответствие методов типу делегата не требуется. Дополнительные сведения см. в разделе [Использование вариативности в делегатах](../concepts/covariance-contravariance/using-variance-in-delegates.md).  
  
- В C# версии 2.0 введена концепция [анонимных методов](../../language-reference/operators/delegate-operator.md), которые позволяют передавать блоки кода в виде параметров вместо использования отдельно определенного метода. В C# 3.0 для краткой записи встроенных блоков кода введены лямбда-выражения. В результате компиляции как анонимных методов, так и лямбда-выражений (в определенном контексте) получаются типы делегатов. В настоящее время эти возможности называются анонимными возможностями. Дополнительные сведения о лямбда-выражениях см. в разделе [Лямбда-выражения](../../language-reference/operators/lambda-expressions.md).
  
## <a name="in-this-section"></a>В этом разделе  
  
- [Использование делегатов](./using-delegates.md)  
  
- [Использование делегатов вместо интерфейсов (руководство по программированию на C#)](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms173173(v=vs.100))  
  
- [Делегаты с именованными методами и делегаты с анонимными методами](./delegates-with-named-vs-anonymous-methods.md)  
  
- [Использование расхождения в делегатах](../concepts/covariance-contravariance/using-variance-in-delegates.md)  
  
- [Практическое руководство. Объединение делегатов (многоадресные делегаты)](./how-to-combine-delegates-multicast-delegates.md)  
  
- [Практическое руководство. Объявление, создание и использование делегата](./how-to-declare-instantiate-and-use-a-delegate.md)

## <a name="c-language-specification"></a>Спецификация языка C#  

Дополнительные сведения см. в разделе [Делегаты](~/_csharplang/spec/delegates.md) в [Спецификации языка C#](/dotnet/csharp/language-reference/language-specification/introduction). Спецификация языка является предписывающим источником информации о синтаксисе и использовании языка C#.
  
## <a name="featured-book-chapters"></a>Главы в популярных книгах  
 [Делегаты, события и лямбда-выражения](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff518994%28v=orm.10%29) в [справочном руководстве по C# 3.0, третье издание. Более 250 решений для программистов на C# 3.0](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff518995%28v=orm.10%29)  
  
 [Делегаты и события](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652490%28v=orm.10%29) в [изучении C# 3.0. Овладение основными понятиями C# 3.0](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652493%28v=orm.10%29)  
  
## <a name="see-also"></a>См. также

- <xref:System.Delegate>
- [Руководство по программированию на C#](../index.md)
- [События](../events/index.md)
