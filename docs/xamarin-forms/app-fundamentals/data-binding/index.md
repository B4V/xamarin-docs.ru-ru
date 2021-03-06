---
title: Привязка данных в Xamarin.Forms
description: Привязка данных — это метод связывания свойства двух объектов, чтобы изменения в одном свойстве автоматически отражаются в другое свойство. Привязка данных является составной частью архитектуры Model-View-ViewModel (MVVM) приложения.
ms.prod: xamarin
ms.assetid: 938E85C8-521D-43B9-92CB-D591A06D98A6
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/23/2018
ms.openlocfilehash: def97ab77781c7a7156d4c4178097184614f3e8b
ms.sourcegitcommit: 7f6127c2f425fadc675b77d14de7a36103cff675
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2018
ms.locfileid: "35240357"
---
# <a name="xamarinforms-data-binding"></a>Привязка данных в Xamarin.Forms

_Привязка данных — это метод связывания свойства двух объектов, чтобы изменения в одном свойстве автоматически отражаются в другое свойство. Привязка данных является составной частью архитектуры Model-View-ViewModel (MVVM) приложения._

## <a name="the-data-linking-problem"></a>Проблема связывания данных

Приложение Xamarin.Forms состоит из одной или нескольких страниц, как правило, каждый из которых содержит несколько объектов пользовательского интерфейса называется *представления*. Одно из основных задач программы — оставить эти представления синхронизации и для отслеживания различных значений или выбранных элементов, которые они представляют. Часто представления представляют значения из базового источника данных, и пользователь управляет эти представления, чтобы изменить эти данные. При изменении представления, базовые данные должны отражать изменения, и аналогично, при изменении базовых данных, это изменение отражается в представлении.

Для обработки этого задания успешно, программа должна уведомляется об изменениях в этих представлениях или базовых данных. Распространенным решением является определение событий, которые указывают, когда происходит изменение. Обработчик событий можно установить, уведомления об этих изменениях. Она отвечает, передачи данных от одного объекта к другому. Тем не менее когда существует множество представлений, также должны многие обработчики событий и работе подключается большого объема кода.

## <a name="the-data-binding-solution"></a>Решение привязки данных

Привязка данных автоматизирует этого задания и избавляет от необходимости обработчики событий. (События, по-прежнему необходимо, тем не менее, так как они используются для инфраструктуры привязки данных.) Привязки данных можно реализовать в коде или в XAML, но они гораздо больше распространен в XAML, где они позволяют уменьшить размер файла кода. Заменяя процедурного кода в обработчиках событий декларативного кода или разметки, упрощенный и уточнено приложение.

Один из двух объектов, относящиеся к привязке данных почти всегда является элементом, который является производным от `View` и формирует часть визуального интерфейса страницы. Другой объект равен:

- Другой `View` класс, производный от, обычно на одной странице.
- Объект, в файле кода.

В демонстрационных программ, например, в [ **DataBindingDemos** ](https://developer.xamarin.com/samples/xamarin-forms/DataBindingDemos/) пример привязки данных между двумя `View` производные часто отображаются в рамках простоты и ясности. Тем не менее, те же принципы могут применяться к привязки данных между `View` и других объектов. При построении приложения с помощью архитектуры Model-View-ViewModel (MVVM), класс с базовыми данными часто называется ViewModel.

В следующей серии статей рассматриваются привязки данных:

## <a name="basic-bindingsbasic-bindingsmd"></a>[Основные привязки](basic-bindings.md)

Узнайте, отличается от целевого объекта привязки данных источника и простые данные привязки в коде и XAML.

## <a name="binding-modebinding-modemd"></a>[Режим привязки](binding-mode.md)

Узнайте, как режим привязки могут контролировать поток данных между двумя объектами.

## <a name="string-formattingstring-formattingmd"></a>[Форматирование строки](string-formatting.md)

Используйте привязку данных для форматирования и отображения объектов в виде строк.

## <a name="binding-pathbinding-pathmd"></a>[Путь привязки](binding-path.md)

Детального изучения `Path` свойство привязки данных для доступа к подчиненные свойства и элементы коллекции.

## <a name="binding-value-convertersconvertersmd"></a>[Привязка преобразователей значений](converters.md)

Используйте привязка преобразователей значений для изменения значений в рамках привязок данных.

## <a name="binding-fallbacksbinding-fallbacksmd"></a>[В случае ошибки привязки](binding-fallbacks.md)

Сделаем еще надежнее привязки данных путем определения возврата значений, используемых при сбое процесса привязки.

## <a name="the-command-interfacecommandingmd"></a>[Командный интерфейс](commanding.md)

Реализуйте `Command` свойства с помощью привязки данных.

## <a name="compiled-bindingscompiled-bindingsmd"></a>[Скомпилированный привязки](compiled-bindings.md)

Используйте скомпилированные привязки для повышения производительности привязки данных.

## <a name="related-links"></a>Связанные ссылки

- [Демонстрации, привязка данных (пример)](https://developer.xamarin.com/samples/xamarin-forms/DataBindingDemos/)
- [Данные привязки Глава из книги по Xamarin.Forms](~/xamarin-forms/creating-mobile-apps-xamarin-forms/summaries/chapter16.md)
- [Расширения разметки XAML](~/xamarin-forms/xaml/markup-extensions/index.md)
