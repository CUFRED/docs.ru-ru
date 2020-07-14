---
title: Службы XAML
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], System.Xaml concepts
- XAML Services in WPF [XAML Services]
- System.Xaml [XAML Services], conceptual documentation
ms.assetid: 0e11f386-808c-4eae-9ba6-029ad7ba2211
ms.openlocfilehash: bfb3efb479668bcd70a3ce87b80253a73c18bb51
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2020
ms.locfileid: "85840322"
---
# <a name="xaml-services"></a><span data-ttu-id="a39a9-102">Службы XAML</span><span class="sxs-lookup"><span data-stu-id="a39a9-102">XAML Services</span></span>

<span data-ttu-id="a39a9-103">В этом разделе описываются возможности набора технологий, известного как службы XAML для .NET.</span><span class="sxs-lookup"><span data-stu-id="a39a9-103">This topic describes the capabilities of a technology set known as .NET XAML Services.</span></span> <span data-ttu-id="a39a9-104">Большинство рассматриваемых здесь служб и API размещается в сборке `System.Xaml`.</span><span class="sxs-lookup"><span data-stu-id="a39a9-104">The majority of the services and APIs described are located in the assembly `System.Xaml`.</span></span> <span data-ttu-id="a39a9-105">Службы включают модули чтения и записи, классы схемы и поддержку схем, фабрики, атрибуты классов, встроенную поддержку языка XAML, а также другие возможности языка XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-105">Services include readers and writers, schema classes and schema support, factories, attributing of classes, XAML language intrinsic support, and other XAML language features.</span></span>

## <a name="about-this-documentation"></a><span data-ttu-id="a39a9-106">Сведения об этой документации</span><span class="sxs-lookup"><span data-stu-id="a39a9-106">About This Documentation</span></span>

<span data-ttu-id="a39a9-107">Для изучения концептуальной документации по службам XAML для .NET требуется опыт работы с языком XAML и знание принципов его применения на различных платформах, таких как Windows Presentation Foundation (WPF) или Windows Workflow Foundation, а также в отдельных функциональных областях, например при работе с компонентами пользовательской настройки сборки <xref:Microsoft.Build.Framework.XamlTypes>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-107">Conceptual documentation for .NET XAML Services assumes that you have previous experience with the XAML language and how it might apply to a specific framework, for example Windows Presentation Foundation (WPF) or Windows Workflow Foundation, or a specific technology feature area, for example the build customization features in <xref:Microsoft.Build.Framework.XamlTypes>.</span></span> <span data-ttu-id="a39a9-108">В этой документации не затрагиваются основы применения XAML как языка разметки, термины синтаксиса XAML и другие сведения начального уровня.</span><span class="sxs-lookup"><span data-stu-id="a39a9-108">This documentation does not attempt to explain the basics of XAML as a markup language, XAML syntax terminology, or other introductory material.</span></span> <span data-ttu-id="a39a9-109">Вместо этого в ней делается акцент на применении служб XAML для .NET, включенных в библиотеку сборки System.Xaml.</span><span class="sxs-lookup"><span data-stu-id="a39a9-109">Instead, this documentation focuses on specifically using .NET XAML Services that are enabled in the System.Xaml assembly library.</span></span> <span data-ttu-id="a39a9-110">Большинство этих API предназначено для сценариев, связанных с интеграцией и расширяемостью языка XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-110">Most of these APIs are for scenarios of XAML language integration and extensibility.</span></span> <span data-ttu-id="a39a9-111">К ним можно отнести следующие:</span><span class="sxs-lookup"><span data-stu-id="a39a9-111">This might include any of the following scenarios:</span></span>

- <span data-ttu-id="a39a9-112">Расширение возможностей базовых модулей чтения и записи XAML (непосредственная обработка потока узлов XAML; получение собственных модулей чтения или записи XAML).</span><span class="sxs-lookup"><span data-stu-id="a39a9-112">Extending the capabilities of the base XAML readers or XAML writers (processing the XAML node stream directly; deriving your own XAML reader or XAML writer).</span></span>

- <span data-ttu-id="a39a9-113">Определение настраиваемых типов для работы с XAML, которые не зависят от конкретной платформы, а также настройка атрибутов таких типов для передачи характеристик их системы типов XAML в службы XAML для .NET.</span><span class="sxs-lookup"><span data-stu-id="a39a9-113">Defining XAML-usable custom types that do not have specific framework dependencies, and attributing the types to convey their XAML type system characteristics to .NET XAML Services.</span></span>

- <span data-ttu-id="a39a9-114">Размещение модулей чтения или записи XAML в качестве компонента приложения, такого как визуальный конструктор или интерактивный редактор для источников разметки XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-114">Hosting XAML readers or XAML writers as a component of an application, such as a visual designer or interactive editor for XAML markup sources.</span></span>

- <span data-ttu-id="a39a9-115">Написание преобразователей значений XAML (расширения разметки; преобразователи для пользовательских типов).</span><span class="sxs-lookup"><span data-stu-id="a39a9-115">Writing XAML value converters (markup extensions; type converters for custom types).</span></span>

- <span data-ttu-id="a39a9-116">Определение пользовательского контекста схемы XAML (с использованием альтернативных методов загрузки сборки для резервных источников типов; с использованием методов поиска известных типов вместо постоянного отражения сборок; использование концепций загруженных сборок, не использующих общеязыковую среду выполнения (CLR) `AppDomain`, и связанной с ними модели безопасности).</span><span class="sxs-lookup"><span data-stu-id="a39a9-116">Defining a custom XAML schema context (using alternate assembly-loading techniques for backing type sources; using known-types lookup techniques instead of always reflecting assemblies; using loaded assembly concepts that do not use the common language runtime (CLR) `AppDomain` and its associated security model).</span></span>

- <span data-ttu-id="a39a9-117">Расширение базовой системы типов XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-117">Extending the base XAML type system.</span></span>

- <span data-ttu-id="a39a9-118">Применение методик `Lookup` или `Invoker` для воздействия на систему типов и принципы оценки резервных типов.</span><span class="sxs-lookup"><span data-stu-id="a39a9-118">Using the `Lookup` or `Invoker` techniques to influence the XAML type system and how type backings are evaluated.</span></span>

<span data-ttu-id="a39a9-119">Сведения начального уровня о языке XAML можно найти в статье [Общие сведения о языке XAML (WPF)](../fundamentals/xaml.md).</span><span class="sxs-lookup"><span data-stu-id="a39a9-119">If you are looking for introductory material on XAML as a language, you might try [XAML Overview (WPF)](../fundamentals/xaml.md).</span></span> <span data-ttu-id="a39a9-120">В ней язык XAML рассматривается с точки зрения пользователей, не знакомых с платформой Windows Presentation Foundation (WPF) или использованием разметки и возможностей этого языка.</span><span class="sxs-lookup"><span data-stu-id="a39a9-120">That topic discusses XAML for an audience that is new both to Windows Presentation Foundation (WPF) and also to using XAML markup and XAML language features.</span></span> <span data-ttu-id="a39a9-121">Также для начала работы рекомендуется ознакомиться с материалами, представленными в [спецификации языка XAML](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10)).</span><span class="sxs-lookup"><span data-stu-id="a39a9-121">Another useful document is the introductory material in the [XAML language specification](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10)).</span></span>

## <a name="net-xaml-services-and-systemxaml-in-the-net-architecture"></a><span data-ttu-id="a39a9-122">Службы XAML для .NET и `System.Xaml` в архитектуре .NET</span><span class="sxs-lookup"><span data-stu-id="a39a9-122">.NET XAML Services and `System.Xaml` in the .NET Architecture</span></span>

<span data-ttu-id="a39a9-123">В службах XAML для .NET и сборке `System.Xaml` определяется большая часть компонентов, необходимых для поддержки возможностей языка XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-123">.NET XAML Services and the `System.Xaml` assembly define much of what is needed for supporting XAML language features.</span></span> <span data-ttu-id="a39a9-124">К ним относятся базовые классы для модулей чтения и записи XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-124">This includes base classes for XAML readers and XAML writers.</span></span> <span data-ttu-id="a39a9-125">Ключевой возможностью, которая была добавлена в службах XAML для .NET и отсутствовала в реализациях XAML для конкретных платформ, является представление системы типов для XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-125">The most important feature added to .NET XAML Services that was not present in any of the framework-specific XAML implementations is a type system representation for XAML.</span></span> <span data-ttu-id="a39a9-126">В этом представлении системы типов язык XAML рассматривается с использованием объектно-ориентированного подхода, который фокусируется на возможностях XAML и не учитывает зависимости от реализованных на конкретных платформах возможностей.</span><span class="sxs-lookup"><span data-stu-id="a39a9-126">The type system representation presents XAML in an object-oriented way that centers on XAML capabilities without taking dependencies on specific capabilities of frameworks.</span></span>

<span data-ttu-id="a39a9-127">Система типов XAML не ограничивается формой разметки или характеристиками времени выполнения, свойственными XAML, а также какой-либо конкретной резервной системы типов.</span><span class="sxs-lookup"><span data-stu-id="a39a9-127">The XAML type system is not limited by the markup form or run-time specifics of the XAML origin; nor is it limited by any specific backing type system.</span></span> <span data-ttu-id="a39a9-128">Система типов XAML включает объектные представления типов, членов, контекстов схемы XAML, концепций уровня XML и других концепций языка XAML, а также встроенных возможностей XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-128">The XAML type system includes object representations for types, members, XAML schema contexts, XML-level concepts, and other XAML language concepts or XAML intrinsics.</span></span> <span data-ttu-id="a39a9-129">Применение или расширение системы типов XAML позволяет создавать производные классы от таких классов, как модули чтения и записи XAML, а также расширять функциональные возможности представления XAML для поддержки конкретных функций, реализуемых в рамках платформы, технологии или приложения, которые используют или генерируют XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-129">Using or extending the XAML type system makes it possible to derive from classes like XAML readers and XAML writers, and extend the functionality of XAML representations into specific features enabled by a framework, a technology, or an application that consumes or emits XAML.</span></span> <span data-ttu-id="a39a9-130">Концепция контекста схемы XAML позволяет реализовать эффективные операции записи графа объектов на основе сочетания реализации модуля записи объектов XAML, резервной системы типов для соответствующей технологии, которая указывается в сведениях о сборке в контексте, а также источника узлов XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-130">The concept of a XAML schema context enables practical object graph write operations from the combination of a XAML object writer implementation, a technology's backing type system as communicated through assembly information in the context, and the XAML node source.</span></span> <span data-ttu-id="a39a9-131">Дополнительные сведения о концепции схемы XAML</span><span class="sxs-lookup"><span data-stu-id="a39a9-131">For more information on the XAML schema concept.</span></span> <span data-ttu-id="a39a9-132">см. в разделе [Контекст схемы языка XAML по умолчанию и контекст схемы языка XAML WPF](default-schema-context.md).</span><span class="sxs-lookup"><span data-stu-id="a39a9-132">see [Default XAML Schema Context and WPF XAML Schema Context](default-schema-context.md).</span></span>

## <a name="xaml-node-streams-xaml-readers-and-xaml-writers"></a><span data-ttu-id="a39a9-133">Потоки узлов XAML, модули чтения XAML и модули записи XAML</span><span class="sxs-lookup"><span data-stu-id="a39a9-133">XAML Node Streams, XAML Readers, and XAML Writers</span></span>

<span data-ttu-id="a39a9-134">Чтобы понять роль, которую службы XAML для .NET играют в отношениях между языком XAML и конкретными использующими его технологиями, важно ознакомиться с концепцией потока узлов XAML, а также ее влиянием на определение API и терминологии.</span><span class="sxs-lookup"><span data-stu-id="a39a9-134">To understand the role that .NET XAML Services plays in the relationship between the XAML language and specific technologies that use XAML as a language, it is helpful to understand the concept of a XAML node stream and how that concept shapes the API and terminology.</span></span> <span data-ttu-id="a39a9-135">Поток узлов XAML представляет собой концептуальный промежуточный уровень между представлением языка XAML и графом объектов, который представляет или определяет XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-135">The XAML node stream is a conceptual intermediate between a XAML language representation and the object graph that the XAML represents or defines.</span></span>

- <span data-ttu-id="a39a9-136">Модуль чтения XAML — это сущность, которая реализует определенную форму обработки XAML и генерирует поток узлов XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-136">A XAML reader is an entity that processes XAML in some form, and produces a XAML node stream.</span></span> <span data-ttu-id="a39a9-137">В API модуль чтения XAML представлен базовым классом <xref:System.Xaml.XamlReader>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-137">In the API, a XAML reader is represented by the base class <xref:System.Xaml.XamlReader>.</span></span>

- <span data-ttu-id="a39a9-138">Модуль записи XAML — это сущность, которая обрабатывает поток узлов XAML и генерирует какие-либо другие сущности.</span><span class="sxs-lookup"><span data-stu-id="a39a9-138">A XAML writer is an entity that processes a XAML node stream and produces something else.</span></span> <span data-ttu-id="a39a9-139">В API модуль записи XAML представлен базовым классом <xref:System.Xaml.XamlWriter>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-139">In the API, a XAML writer is represented by the base class <xref:System.Xaml.XamlWriter>.</span></span>

  <span data-ttu-id="a39a9-140">Наиболее распространенными сценариями использования XAML являются загрузка XAML для создания экземпляра графа объектов из приложения или средства, а также создание представления XAML (как правило, в форме разметки, сохраненной в текстовом файле).</span><span class="sxs-lookup"><span data-stu-id="a39a9-140">The two most common scenarios involving XAML are loading XAML to instantiate an object graph, and saving an object graph from an application or tool and producing a XAML representation (typically in markup form saved as text file).</span></span> <span data-ttu-id="a39a9-141">Сценарий загрузки XAML и создания графа объектов в этой документации зачастую называется путем загрузки.</span><span class="sxs-lookup"><span data-stu-id="a39a9-141">Loading XAML and creating an object graph is often referred to in this documentation as the load path.</span></span> <span data-ttu-id="a39a9-142">Сценарий сохранения или сериализации существующего графа объектов в XAML в этой документации часто называется путем сохранения.</span><span class="sxs-lookup"><span data-stu-id="a39a9-142">Saving or serializing an existing object graph to XAML is often referred to in this documentation as the save path.</span></span>

  <span data-ttu-id="a39a9-143">Самый распространенный тип пути загрузки можно описать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a39a9-143">The most common type of load path can be described as follows:</span></span>

- <span data-ttu-id="a39a9-144">Начальное представление XAML в формате XML с кодировкой UTF сохраняется в текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="a39a9-144">Start with a XAML representation, in UTF-encoded XML format and saved as a text file.</span></span>

- <span data-ttu-id="a39a9-145">Полученный файл XAML загружается в <xref:System.Xaml.XamlXmlReader>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-145">Load that XAML into <xref:System.Xaml.XamlXmlReader>.</span></span> <span data-ttu-id="a39a9-146"><xref:System.Xaml.XamlXmlReader> — это подкласс <xref:System.Xaml.XamlReader>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-146"><xref:System.Xaml.XamlXmlReader> is a <xref:System.Xaml.XamlReader> subclass.</span></span>

- <span data-ttu-id="a39a9-147">В результате получается поток узлов XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-147">The result is a XAML node stream.</span></span> <span data-ttu-id="a39a9-148">Отдельные узлы потока узлов XAML можно назначать с помощью API <xref:System.Xaml.XamlXmlReader> / <xref:System.Xaml.XamlReader>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-148">You can access individual nodes of the XAML node stream using <xref:System.Xaml.XamlXmlReader> / <xref:System.Xaml.XamlReader> API.</span></span> <span data-ttu-id="a39a9-149">Чаще всего в этом случае осуществляется продвижение по потоку узлов XAML с последовательной обработкой каждого узла как "текущей записи".</span><span class="sxs-lookup"><span data-stu-id="a39a9-149">The most typical operation here is to advance through the XAML node stream, processing each node using a "current record" metaphor.</span></span>

- <span data-ttu-id="a39a9-150">Полученные узлы передаются из потока узлов XAML в API <xref:System.Xaml.XamlObjectWriter>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-150">Pass the resulting nodes from the XAML node stream to a <xref:System.Xaml.XamlObjectWriter> API.</span></span> <span data-ttu-id="a39a9-151"><xref:System.Xaml.XamlObjectWriter> — это подкласс <xref:System.Xaml.XamlWriter>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-151"><xref:System.Xaml.XamlObjectWriter> is a <xref:System.Xaml.XamlWriter> subclass.</span></span>

- <span data-ttu-id="a39a9-152"><xref:System.Xaml.XamlObjectWriter> осуществляет запись графа объектов по одному объекту за раз в соответствии с ходом обработки исходного потока узлов XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-152">The <xref:System.Xaml.XamlObjectWriter> writes an object graph, one object at a time, in accordance to progress through the source XAML node stream.</span></span> <span data-ttu-id="a39a9-153">Запись объекта осуществляется с использованием контекста схемы XAML и реализации, которая имеет доступ ко всем сборкам и типам резервной системы типов и платформы.</span><span class="sxs-lookup"><span data-stu-id="a39a9-153">Object writing is done with the assistance of a XAML schema context and an implementation that can access the assemblies and types of a backing type system and framework.</span></span>

- <span data-ttu-id="a39a9-154">В конце потока узлов XAML вызывается <xref:System.Xaml.XamlObjectWriter.Result%2A> для получения корневого объекта графа объектов.</span><span class="sxs-lookup"><span data-stu-id="a39a9-154">Call <xref:System.Xaml.XamlObjectWriter.Result%2A> at the end of the XAML node stream to obtain the root object of the object graph.</span></span>

  <span data-ttu-id="a39a9-155">Самый распространенный тип пути сохранения можно описать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a39a9-155">The most common type of save path can be described as follows:</span></span>

- <span data-ttu-id="a39a9-156">Для начала принимается граф объектов времени выполнения для всего приложения, содержимое и состояние пользовательского интерфейса во время выполнения, либо частичный сегмент общего представления объекта приложения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="a39a9-156">Start with the object graph of an entire application run time, the UI content and state of a run time, or a smaller segment of an overall application's object representation at run time.</span></span>

- <span data-ttu-id="a39a9-157">Объекты загружаются из логического начального объекта, например корневого объекта приложения или документа, в <xref:System.Xaml.XamlObjectReader>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-157">From a logical start object, such as an application root or document root, load the objects into <xref:System.Xaml.XamlObjectReader>.</span></span> <span data-ttu-id="a39a9-158"><xref:System.Xaml.XamlObjectReader> — это подкласс <xref:System.Xaml.XamlReader>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-158"><xref:System.Xaml.XamlObjectReader> is a <xref:System.Xaml.XamlReader> subclass.</span></span>

- <span data-ttu-id="a39a9-159">В результате получается поток узлов XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-159">The result is a XAML node stream.</span></span> <span data-ttu-id="a39a9-160">Отдельные узлы потока узлов XAML можно назначать с помощью API <xref:System.Xaml.XamlObjectReader> и <xref:System.Xaml.XamlReader>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-160">You can access individual nodes of the XAML node stream using <xref:System.Xaml.XamlObjectReader> and <xref:System.Xaml.XamlReader> API.</span></span> <span data-ttu-id="a39a9-161">Чаще всего в этом случае осуществляется продвижение по потоку узлов XAML с последовательной обработкой каждого узла как "текущей записи".</span><span class="sxs-lookup"><span data-stu-id="a39a9-161">The most typical operation here is to advance through the XAML node stream, processing each node using a "current record" metaphor.</span></span>

- <span data-ttu-id="a39a9-162">Полученные узлы передаются из потока узлов XAML в API <xref:System.Xaml.XamlXmlWriter>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-162">Pass the resulting nodes from the XAML node stream to a <xref:System.Xaml.XamlXmlWriter> API.</span></span> <span data-ttu-id="a39a9-163"><xref:System.Xaml.XamlXmlWriter> — это подкласс <xref:System.Xaml.XamlWriter>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-163"><xref:System.Xaml.XamlXmlWriter> is a <xref:System.Xaml.XamlWriter> subclass.</span></span>

- <span data-ttu-id="a39a9-164"><xref:System.Xaml.XamlXmlWriter> записывает XAML в формате XML в кодировке UTF.</span><span class="sxs-lookup"><span data-stu-id="a39a9-164">The <xref:System.Xaml.XamlXmlWriter> writes XAML in an XML UTF encoding.</span></span> <span data-ttu-id="a39a9-165">Полученные данные можно сохранить в виде текстового файла, потока или в другой форме.</span><span class="sxs-lookup"><span data-stu-id="a39a9-165">You can save this as a text file, as a stream, or in other forms.</span></span>

- <span data-ttu-id="a39a9-166">Для получения конечных выходных данных вызывается <xref:System.Xaml.XamlXmlWriter.Flush%2A>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-166">Call <xref:System.Xaml.XamlXmlWriter.Flush%2A> to obtain the final output.</span></span>

<span data-ttu-id="a39a9-167">Дополнительные сведения о концепциях потока узлов XAML см. в статье [Общее представление о понятиях и структурах потока узлов XAML](understanding-xaml-node-stream-structures-and-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="a39a9-167">For more information about XAML node stream concepts, see [Understanding XAML Node Stream Structures and Concepts](understanding-xaml-node-stream-structures-and-concepts.md).</span></span>

### <a name="the-xamlservices-class"></a><span data-ttu-id="a39a9-168">Класс XamlServices</span><span class="sxs-lookup"><span data-stu-id="a39a9-168">The XamlServices Class</span></span>

<span data-ttu-id="a39a9-169">Поток узлов XAML требуется не во всех случаях.</span><span class="sxs-lookup"><span data-stu-id="a39a9-169">It is not always necessary to deal with a XAML node stream.</span></span> <span data-ttu-id="a39a9-170">Если вам требуется базовый путь загрузки или сохранения, вы можете использовать API, реализованные в классе <xref:System.Xaml.XamlServices>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-170">If you want a basic load path or a basic save path, you can use APIs in the <xref:System.Xaml.XamlServices> class.</span></span>

- <span data-ttu-id="a39a9-171">Путь загрузки реализуется с использованием различных сигнатур <xref:System.Xaml.XamlServices.Load%2A>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-171">Various signatures of <xref:System.Xaml.XamlServices.Load%2A> implement a load path.</span></span> <span data-ttu-id="a39a9-172">Можно загрузить файл или поток, либо загрузить <xref:System.Xml.XmlReader>, <xref:System.IO.TextReader>или <xref:System.Xaml.XamlReader> для заключения входных данных XAML в оболочку путем загрузки с интерфейсами API модуля чтения.</span><span class="sxs-lookup"><span data-stu-id="a39a9-172">You can either load a file or stream, or can load an <xref:System.Xml.XmlReader>, <xref:System.IO.TextReader> or <xref:System.Xaml.XamlReader> that wrap your XAML input by loading with that reader's APIs.</span></span>

- <span data-ttu-id="a39a9-173">Методы <xref:System.Xaml.XamlServices.Save%2A> с разными сигнатурами принимают граф объектов на вход, а выходом является поток, файл или экземпляр <xref:System.Xml.XmlWriter>/<xref:System.IO.TextWriter>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-173">Various signatures of <xref:System.Xaml.XamlServices.Save%2A> save an object graph and produce output as a stream, file, or <xref:System.Xml.XmlWriter>/<xref:System.IO.TextWriter> instance.</span></span>

- <span data-ttu-id="a39a9-174"><xref:System.Xaml.XamlServices.Transform%2A> преобразует XAML, связывая путь загрузки и путь сохранения в одну операцию.</span><span class="sxs-lookup"><span data-stu-id="a39a9-174"><xref:System.Xaml.XamlServices.Transform%2A> converts XAML by linking a load path and a save path as a single operation.</span></span> <span data-ttu-id="a39a9-175">Для <xref:System.Xaml.XamlReader> и <xref:System.Xaml.XamlWriter> могут использоваться другой контекст схемы или другая резервная система типов, что повлияет на преобразование полученного XAML-кода.</span><span class="sxs-lookup"><span data-stu-id="a39a9-175">A different schema context or different backing type system could be used for <xref:System.Xaml.XamlReader> and <xref:System.Xaml.XamlWriter>, which is what influences how the resulting XAML is transformed.</span></span>

<span data-ttu-id="a39a9-176">Дополнительные сведения об использовании <xref:System.Xaml.XamlServices> см. в статье [Класс XAMLServices и чтение или запись базового кода XAML](basic-reading-writing.md).</span><span class="sxs-lookup"><span data-stu-id="a39a9-176">For more information about how to use <xref:System.Xaml.XamlServices>, see [XAMLServices Class and Basic XAML Reading or Writing](basic-reading-writing.md).</span></span>

## <a name="xaml-type-system"></a><span data-ttu-id="a39a9-177">Система типов XAML</span><span class="sxs-lookup"><span data-stu-id="a39a9-177">XAML Type System</span></span>

<span data-ttu-id="a39a9-178">Система типов XAML предоставляет API-интерфейсы, необходимые для работы с отдельными узлами потока узлов XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-178">The XAML type system provides the APIs that are required to work with a given individual node of a XAML node stream.</span></span>

<span data-ttu-id="a39a9-179"><xref:System.Xaml.XamlType> — это представление объекта, который обрабатывается между начальным и конечным узлом объекта.</span><span class="sxs-lookup"><span data-stu-id="a39a9-179"><xref:System.Xaml.XamlType> is the representation for an object - what you are processing between a start object node and end object node.</span></span>

<span data-ttu-id="a39a9-180"><xref:System.Xaml.XamlMember> — это представление члена объекта, который обрабатывается между начальным и конечным членом узла.</span><span class="sxs-lookup"><span data-stu-id="a39a9-180"><xref:System.Xaml.XamlMember> is the representation for a member of an object - what you are processing between a start member node and end member node.</span></span>

<span data-ttu-id="a39a9-181">API-интерфейсы, например <xref:System.Xaml.XamlType.GetAllMembers%2A>, <xref:System.Xaml.XamlType.GetMember%2A> и <xref:System.Xaml.XamlMember.DeclaringType%2A>, сообщают о связи между <xref:System.Xaml.XamlType> и <xref:System.Xaml.XamlMember>.</span><span class="sxs-lookup"><span data-stu-id="a39a9-181">APIs such as <xref:System.Xaml.XamlType.GetAllMembers%2A> and <xref:System.Xaml.XamlType.GetMember%2A> and <xref:System.Xaml.XamlMember.DeclaringType%2A> report the relationships between a <xref:System.Xaml.XamlType> and <xref:System.Xaml.XamlMember>.</span></span>

<span data-ttu-id="a39a9-182">По умолчанию (например, в службах XAML для .NET) система типов XAML реализуется на основе общеязыковой среды выполнения (CLR) и статического анализа типов CLR в сборках посредством отражения.</span><span class="sxs-lookup"><span data-stu-id="a39a9-182">The default behavior of the XAML type system as implemented by .NET XAML Services is based on the common language runtime (CLR), and static analysis of CLR types in assemblies by using reflection.</span></span> <span data-ttu-id="a39a9-183">Соответственно, для конкретного типа CLR в определяемой по умолчанию реализации система типов XAML может предоставлять схему XAML этого типа и его членов, а также сообщать о связи между ними в контексте системы типов XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-183">Therefore, for a specific CLR type, the default implementation of the XAML type system can expose the XAML schema of that type and its members and report it in terms of the XAML type system.</span></span> <span data-ttu-id="a39a9-184">В системе типов XAML по умолчанию концепция возможности назначения типов сопоставляется с принципами наследования CLR, а понятия экземпляров, типов значений и т. д. — с соответствующими понятиями и функциями CLR.</span><span class="sxs-lookup"><span data-stu-id="a39a9-184">In the default XAML type system, the concept of assignability of types is mapped onto CLR inheritance, and the concepts of instances, value types, and so on, are also mapped to the supporting behaviors and features of the CLR.</span></span>

## <a name="reference-for-xaml-language-features"></a><span data-ttu-id="a39a9-185">Справочник по возможностям языка XAML</span><span class="sxs-lookup"><span data-stu-id="a39a9-185">Reference for XAML Language Features</span></span>

<span data-ttu-id="a39a9-186">Чтобы обеспечить поддержку XAML, в службах XAML для .NET используется специальная реализация концепций языка XAML, определяемая в пространстве имен XAML языка XAML.</span><span class="sxs-lookup"><span data-stu-id="a39a9-186">To support XAML, .NET XAML Services provides specific implementation of XAML language concepts as defined for the XAML language XAML namespace.</span></span> <span data-ttu-id="a39a9-187">Эти концепции задокументированы на соответствующих страницах справочника.</span><span class="sxs-lookup"><span data-stu-id="a39a9-187">These are documented as specific reference pages.</span></span> <span data-ttu-id="a39a9-188">В документации возможности языка рассматриваются с точки зрения их поведения при обработке модулем чтения или записи XAML, который определяется в службах XAML для .NET.</span><span class="sxs-lookup"><span data-stu-id="a39a9-188">The language features are documented from the perspective of how these language features behave when they are processed by a XAML reader or XAML writer that is defined by .NET XAML Services.</span></span> <span data-ttu-id="a39a9-189">Дополнительные сведения см. в статье [Пространство имен XAML (x:) языка XAML](namespace-language-features.md).</span><span class="sxs-lookup"><span data-stu-id="a39a9-189">For more information, see [XAML Namespace (x:) Language Features](namespace-language-features.md).</span></span>