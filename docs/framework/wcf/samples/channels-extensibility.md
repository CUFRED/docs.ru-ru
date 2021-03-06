---
title: Расширяемость каналов
ms.date: 03/30/2017
ms.assetid: 4cc3b20b-778a-4ae8-b58c-a3822fb13065
ms.openlocfilehash: 9dbae26a548bdc8a8cfb05a3dd90db91475b55ba
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600637"
---
# <a name="channels-extensibility"></a>Расширяемость каналов
В этом разделе содержатся образцы, демонстрирующие пользовательские каналы.  
  
## <a name="in-this-section"></a>В этом разделе  
 [Локальный канал](local-channel.md)  
 Демонстрирует локальный канал, канал транспорта WCF, который используется для связи в пределах одного домена приложения.  
  
 [Надежный защищенный профиль](reliable-secure-profile.md)  
 Демонстрирует, как создать WCF и надежный защищенный профиль (RSP).  
  
 [Настраиваемый диспетчер каналов](custom-channel-dispatcher.md)  
 Демонстрирует построение пользовательского стека каналов путем непосредственной реализации <xref:System.ServiceModel.ServiceHostBase>, а также создание пользовательского диспетчера каналов в среде веб-узла.  
  
 [Фрагментирование канала](chunking-channel.md)  
 Показывает, как ограничить объем памяти, используемой для буферизации больших сообщений, отправляемых с помощью WCF.
  
 [HttpCookieSession](httpcookiesession.md)  
 Демонстрирует, как построить пользовательский канал протокола, который использует для управления сеансами протокол HTTP.  
  
 [Пользовательский перехватчик сообщений](custom-message-interceptor.md)  
 Показано, как реализовать пользовательский элемент привязки, который создает фабрики и прослушиватели каналов для перехвата всех входящих и исходящих сообщений в определенной точке стека времени выполнения.
