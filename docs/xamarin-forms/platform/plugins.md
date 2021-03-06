---
title: Использование и создание подключаемых модулей Xamarin.Forms
description: В этой статье объясняется, как использовать и создавать подключаемые модули Xamarin.Forms. Подключаемые модули обычно используются для простого доступа к собственным возможностям платформы.
ms.prod: xamarin
ms.assetid: 8A06A420-A9D0-4BCB-B9AF-3AEA6A648A8B
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/05/2018
ms.openlocfilehash: 4d121c2dfcca380e1735da1a4ca47c42d1957b8a
ms.sourcegitcommit: ec50c626613f2f9af51a9f4a52781129bcbf3fcb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/05/2018
ms.locfileid: "37854744"
---
# <a name="consuming-and-creating-xamarinforms-plugins"></a>Использование и создание подключаемых модулей Xamarin.Forms

Существует множество функций собственной платформы, которые существуют на всех платформах, но имеет немного другие API-интерфейсы. Одним из способов для разработчиков для использования этих функций является создание абстрактный интерфейс между различными платформами, а затем Реализуйте этот интерфейс на различных платформах. Затем приложение Xamarin.Forms обращается к этих реализаций платформы с помощью [ `DependencyService` ](~/xamarin-forms/app-fundamentals/dependency-service/index.md).

Разработчики могут совместно использовать эту работу, написав _подключаемый модуль_ и публикуя их в NuGet.

> [!NOTE]
> Множество кросс платформенных функций, ранее доступные только через подключаемые модули, теперь являются частью открытым кодом **[Xamarin.Essentials](~/essentials/index.md)** библиотеки. Эти функции включают: состояние аккумулятора, компас, датчиков движения, geolocation, преобразования текста в речь и другие возможности. В будущем **Xamarin.Essentials** будет основным источником кросс платформенные возможности для приложений Xamarin.Forms. Несмотря на то, что разработчикам по-прежнему можно создавать и публиковать подключаемые модули, рекомендуется в дополнение к **Xamarin.Essentials**.

## <a name="finding-and-adding-plugins"></a>Поиск и добавление подключаемых модулей

Xamarin community создала много кроссплатформенных подключаемых модулей совместим с Xamarin.Forms. Большой коллекции можно найти здесь:

[**Подключаемые модули Xamarin**](https://github.com/xamarin/XamarinComponents)

Руководство по добавлению пакетов NuGet в проект, см. в разделе нашим пошаговым руководством на [Включение пакета NuGet в проекте](/visualstudio/mac/nuget-walkthrough/).

## <a name="creating-plugins"></a>Создание подключаемых модулей

Можно также создать и опубликовать свои собственные подключаемые модули как пакеты Nuget (и компоненты Xamarin). Многие существующие подключаемые модули являются открытым исходным кодом, поэтому вы можете просмотреть их код, чтобы понять, как их writtern.

Например, список ниже подключаемые модули имеют открытый исходный код, и они соответствуют некоторые примеры в [ `DependencyService` ](~/xamarin-forms/app-fundamentals/dependency-service/index.md) раздел:

- **Преобразование текста в речь** по Монтеманьо &ndash; [GitHub](https://github.com/jamesmontemagno/TextToSpeechPlugin) и [NuGet  ](https://www.nuget.org/packages/Xam.Plugins.TextToSpeech)
- **Состояние аккумулятора** по Монтеманьо &ndash; [GitHub](https://github.com/jamesmontemagno/BatteryPlugin) и [NuGet](https://www.nuget.org/packages/Xam.Plugin.Battery)

Этими проектами Github можно указать хорошей отправной точкой для создания собственных кроссплатформенных подключаемых модулей, как выполнять эти инструкции для [Создание подключаемого модуля для Xamarin](https://github.com/xamarin/XamarinComponents#create-a-plugin-for-xamarin).

### <a name="structuring-cross-platform-plugin-projects"></a>Структурирование проектов кросс платформенного подключаемого модуля

Несмотря на то, что не существует определенного требований к по созданию пакета NuGet, существуют некоторые рекомендации по созданию пакета для кросс платформенные приложения.

В прошлом кросс платформенного подключаемого модуля обычно состоял из следующих компонентов:

- PCL с интерфейсом, которое представляет API для подключаемого модуля,
- iOS, Android и универсальной платформы Windows (UWP) класса библиотеки, используя реализацию интерфейса.

Чтение Монтеманьо [блога](https://blog.xamarin.com/creating-reusable-plugins-for-xamarin-forms/) описать этот процесс создания подключаемых модулей для Xamarin.

Последнее время подключаемых модулей могут быть создаваться на одной платформе, предназначенный для нескольких платформ. Этот подход рассматривается в Монтеманьо [блога](https://montemagno.com/converting-xamarin-libraries-to-sdk-style-multi-targeted-projects/). Этот подход используется в Монтеманьо подключаемые модули, ссылки выше, а также формат используется в **Xamarin.Essentials**.

Рекомендуется избегать ссылок на Xamarin.Forms непосредственно из подключаемого модуля.
Это может создать проблемы конфликта версий, когда другие разработчики пытаются использовать подключаемый модуль. Вместо этого попробуйте разработать API, таким образом, чтобы он может использоваться любым приложением Xamarin или .NET.

### <a name="publishing-nuget-packages"></a>Публикация пакетов NuGet

Пакеты NuGet имеют **nuspec** файл, который является XML-файл, который определяет, какие части проекта публикуются в пакете. **Nuspec** файл также содержит сведения о пакете, такие как идентификатор, название и авторов.

См. в разделе [документации NuGet](/nuget/create-packages/creating-a-package.md) Дополнительные сведения о создании и публикации пакетов NuGet.

## <a name="related-links"></a>Связанные ссылки

- [Создание многократно используемых подключаемые модули для Xamarin.Forms](https://blog.xamarin.com/creating-reusable-plugins-for-xamarin-forms)
- [Используя & разработке подключаемых модулей для Xamarin (видео)](https://university.xamarin.com/guestlectures/using-developing-plugins-for-xamarin)
