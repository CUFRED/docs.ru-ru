---
title: Выполнение восстановления
description: Выполните восстановление в .NET. Диспетчер ресурсов помогает разрешать прикрепления устойчивых транзакций путем повторного прикрепления участника транзакции после сбоя ресурса.
ms.date: 03/30/2017
ms.assetid: 6dd17bf6-ba42-460a-a44b-8046f52b10d0
ms.openlocfilehash: bb00d2f574cc2651b733f3308cf2ffc6b430cc31
ms.sourcegitcommit: 6219b1e1feccb16d88656444210fed3297f5611e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2020
ms.locfileid: "85141969"
---
# <a name="performing-recovery"></a>Выполнение восстановления
Диспетчер ресурсов обеспечивает разрешение зачислений устойчивых ресурсов в транзакции, повторно зачисляя участника транзакции после сбоя ресурса.  
  
## <a name="the-recovery-process"></a>Процесс восстановления  
 Для зачисления устойчивого ресурса (описываемого реализацией интерфейса <xref:System.Transactions.IEnlistmentNotification>), который способен к восстановлению, необходимо вызвать метод <xref:System.Transactions.Transaction.EnlistDurable%2A>. Кроме того, необходимо предоставить метод <xref:System.Transactions.Transaction.EnlistDurable%2A> с идентификатором диспетчера ресурсов (<xref:System.Guid>), который используется для постоянной отметки участника транзакции в событии сбоя ресурса. По этой причине объект <xref:System.Guid> , предоставляемый первоначальному вызову прикрепления, должен быть идентичен параметру *ресаурцеманажеридентифиер* в <xref:System.Transactions.TransactionManager.Reenlist%2A> вызове во время восстановления. В противном случае возникает исключение <xref:System.Transactions.TransactionException>. Дополнительные сведения о устойчивых прикреплениях см. [в разделе прикрепление ресурсов в качестве участников транзакции](enlisting-resources-as-participants-in-a-transaction.md) .  
  
 Если в фазе подготовки (фазе 1) протокола двухфазной фиксации пользовательская реализация диспетчера ресурсов получает уведомление <xref:System.Transactions.IEnlistmentNotification.Prepare%2A>, она должна создать запись о подготовке в журнале. Запись должна включать всю необходимую информацию для завершения транзакции фиксацией. Доступ к записи подготовки можно получить позже во время восстановления, извлекая <xref:System.Transactions.PreparingEnlistment.RecoveryInformation%2A> свойство обратного вызова *препаринженлистмент* . Создание этой записи в рамках метода <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> не требуется, поскольку диспетчер ресурсов может сделать это в рабочем потоке.  
  
 Процесс восстановления состоит из следующих двух шагов.  
  
### <a name="step-1---reenlist"></a>Шаг 1 - повторное зачисление  
 Диспетчер ресурсов проверяет запись о подготовке для каждого зачисления, которое находится под сомнением. Это выполняется путем проверки свойства <xref:System.Transactions.PreparingEnlistment.RecoveryInformation%2A> обратного вызова <xref:System.Transactions.PreparingEnlistment>, переданного диспетчеру ресурсов в уведомлении <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> в фазе 1.  
  
 Для каждого проверяемого зачисления диспетчер ресурсов вызывает метод <xref:System.Transactions.TransactionManager.Reenlist%2A> для диспетчера транзакций. Этот метод передает уникальный <xref:System.Guid>, идентифицирующий диспетчер ресурсов, а также данные перечисления в массиве байтов. Возвращается новый объект <xref:System.Transactions.Enlistment>. Если в результате повторного зачисления возникает исключение, диспетчеру необходимо повторить попытку через некоторое время.  
  
 Метод <xref:System.Transactions.TransactionManager.Reenlist%2A> следует вызывать только после перезапуска диспетчера ресурсов после сбоя. Кроме того, повторное зачисление следует выполнить только для неразрешенных транзакций, зарегистрированных диспетчером ресурсов в ходе начальной фазы подготовки двухфазной фиксации. Любая попытка вызова этого метода в недопустимое время может привести к ошибочным результатам.  
  
 При повторном зачислении участника с помощью этого метода в зависимости от результата транзакции вызывается соответствующий метод фазы 2 интерфейса <xref:System.Transactions.IEnlistmentNotification> (<xref:System.Transactions.IEnlistmentNotification.Commit%2A>, <xref:System.Transactions.IEnlistmentNotification.Rollback%2A> или <xref:System.Transactions.IEnlistmentNotification.InDoubt%2A>).  
  
### <a name="step-2---completing-the-recovery"></a>Шаг 2 - завершение восстановления  
 После завершения всех повторных зачислений диспетчер транзакций вызывает метод <xref:System.Transactions.TransactionManager.RecoveryComplete%2A>. Этот метод завершает восстановление и информирует диспетчер транзакций о том, что у диспетчера ресурсов больше нет транзакций, находящихся под сомнением. Это позволяет гарантировать, что диспетчер ресурсов не вызовет метод <xref:System.Transactions.TransactionManager.Reenlist%2A> повторно.  
  
 От диспетчера ресурсов не требуется разрешения всех транзакций, находящихся по сомнением, перед повторным зачислением в новые транзакции. Первый шаг можно выполнить в любое время после того, как диспетчер ресурсов установит связь с диспетчером транзакций, но после <xref:System.Transactions.TransactionManager.RecoveryComplete%2A> вызова (шаг 2). шаг 1 не может быть выполнен повторно. Шаг 2 можно выполнить несколько раз без воздействия на результат транзакций.
