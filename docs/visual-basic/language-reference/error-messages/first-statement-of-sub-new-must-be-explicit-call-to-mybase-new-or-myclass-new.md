---
title: 'Первым оператором в этой процедуре Sub New должен быть явный вызов MyBase.New или MyClass.New, так как <constructorname> в базовом классе <baseclassname> класса <derivedclassname> отмечен как устаревший: <errormessage>'
ms.date: 07/20/2015
f1_keywords:
- vbc30920
- bc30920
helpviewer_keywords:
- BC30920
ms.assetid: e47dc755-4294-4368-b813-2177b7677957
ms.openlocfilehash: 33dd15e3f5f5538963597f2b00f4214895e1f47a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403009"
---
# <a name="first-statement-of-this-sub-new-must-be-an-explicit-call-to-mybasenew-or-myclassnew-because-the-constructorname-in-the-base-class-baseclassname-of-derivedclassname-is-marked-obsolete-errormessage"></a>Первым оператором в этой процедуре Sub New должен быть явный вызов MyBase.New или MyClass.New, так как \<constructorname> в базовом классе \<baseclassname> класса \<derivedclassname> отмечен как устаревший: \<errormessage>
Конструктор класса не вызывает явно конструктор базового класса, а вызванный неявно конструктор базового класса помечается атрибутом <xref:System.ObsoleteAttribute> , что является причиной возникновения ошибки.  
  
 Если конструктор производного класса не вызывает конструктор базового класса, Visual Basic пытается создать неявный вызов конструктора базового класса без параметров. Если в базовом классе нет доступного конструктора, который можно вызвать без аргументов, Visual Basic не может создать неявный вызов. В этом случае обязательный конструктор помечается <xref:System.ObsoleteAttribute> атрибутом, поэтому Visual Basic не может вызвать его.  
  
 Вы можете пометить любой программный элемент как неиспользуемый, применив к нему атрибут <xref:System.ObsoleteAttribute> . Если вы это сделаете, вы можете задать для свойства <xref:System.ObsoleteAttribute.IsError%2A> атрибута значение `True` или `False`. Если задать значение `True`, компилятор будет рассматривать попытку использовать элемент как ошибку. Если задать значение `False`или оставить значение по умолчанию `False`, то при попытке использовать элемент компилятор выдаст предупреждение.  
  
 **Идентификатор ошибки:** BC30920  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
1. Проверьте указанное сообщение об ошибке и выполните соответствующее действие.  
  
2. Включите вызов `MyBase.New()` или `MyClass.New()` в качестве первого оператора `Sub New` в производном классе.  
  
## <a name="see-also"></a>См. также раздел

- [Обзор атрибутов](../../programming-guide/concepts/attributes/index.md)
