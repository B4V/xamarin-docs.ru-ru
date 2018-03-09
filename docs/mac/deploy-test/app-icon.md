---
title: "Значок приложения"
description: "В этой статье описано, как создавать изображения, необходимые для использования значков приложения Хamarin.Mac, объединения изображений в файл ICNS и включения значков в проект Xamarin.Mac."
ms.topic: article
ms.prod: xamarin
ms.assetid: 675b9405-d9a7-49f0-94ad-417f10a71d11
ms.technology: xamarin-mac
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/14/2017
ms.openlocfilehash: 742780ad87672bd8a3e2bb3cb66ca582a680d44f
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="application-icon"></a>Значок приложения

_В этой статье описано, как создавать изображения, необходимые для использования значков приложения Хamarin.Mac, объединения изображений в файл ICNS и включения значков в проект Xamarin.Mac._


## <a name="overview"></a>Обзор

При работе с C# и .NET в приложении Xamarin.Mac разработчик может использовать те же средства создания изображений и значков, что и при работе с *Objective-C* и *Xcode*.

Первоклассный значок должен передавать основное назначение приложения Xamarin.Mac и давать представление об ожидаемых действиях при использовании приложения. В этой статье рассматриваются все шаги по созданию необходимых для значка ресурсов изображений, упаковке этих ресурсов в файл `AppIcons.appiconset` и использовании этого файла в приложении Xamarin.Mac.

![Редактор AppIcons.appiconset](app-icon-images/intro01.png "The AppIcons.appiconset editor")


## <a name="application-icon"></a>Значок приложения

Первоклассный значок должен передавать основное назначение приложения Xamarin.Mac и давать представление об ожидаемых действиях при использовании приложения. Каждое приложение macOS должно поддерживать несколько размеров для отображения значка в программе Finder, на панели Dock, панели запуска и в других местах на компьютере.


## <a name="designing-the-icon"></a>Разработка значков

При разработке значков рекомендуется принимать во внимание приведенные далее советы от компании Apple:

- Постарайтесь придать значку реалистичную и уникальную форму.
- Если приложение macOS имеет аналог на платформе iOS, не используйте значок приложения iOS повторно.
- Используйте универсальное и легко узнаваемое изображение.
- Стремитесь к простоте.
- Применяйте цвета и тени с осторожностью, чтобы правильно передать назначение приложения.
- Старайтесь не смешивать реальный текст с _непонятным_ текстом или строками.
- Создайте идеализированную версию темы значка, а не используйте реальную фотографию.
- Избегайте использования элементов пользовательского интерфейса macOS в значках.
- Не используйте в значках копии значков Apple.

Перед разработкой значка приложения Xamarin.Mac ознакомьтесь с разделами о [коллекции значков приложений](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/OSXHIGuidelines/Gallery.html#//apple_ref/doc/uid/20000957-CH88-SW1) и [разработке значков приложений](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/OSXHIGuidelines/Designing.html#//apple_ref/doc/uid/20000957-CH87-SW1) на странице [OS X Human Interface Guidelines](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/OSXHIGuidelines/) (Рекомендации по работе с человеческим интерфейсом OS X) веб-сайта Apple.


## <a name="required-image-sizes-and-filenames"></a>Требуемые размеры изображений и имена файлов

Как и для любого другого ресурса изображения, который разработчик будет использовать в приложении Xamarin.Mac, для значка приложения необходимы версии стандартного разрешения и разрешения Retina. И опять же, как и для любого другого изображения, при именовании файлов значков следует использовать формат `@2x`:

- **Стандартное разрешение**  - _имя_изображения_**.**_расширение_имени_файла_ (например, **icon_512x512.png**).
- **Высокое разрешение**  - _имя_изображения_**@2x.**_расширение_имени_файла_ (например, **icon_512x512@2x.png**).

Например, чтобы указать версию значка приложения 512 x 512, именем файла будет **icon_512x512.png** и **icon_512x512@2x.png**.

Чтобы значок отлично смотрелся во всех местах, где его видят пользователи, необходимо предоставить ресурсы в приведенных ниже размерах:

<table width="100%" border="1px">
<tr>
    <td>имя_файла</td>
    <td>Размер в пикселях</td>
</tr>
<tr>
    <td>icon_512x512@2x.png</td>
    <td>1024 x 1024</td>
</tr>
<tr>
    <td>icon_512x512.png</td>
    <td>512 x 512</td>
</tr>
<tr>
    <td>icon_256x256@2x.png</td>
    <td>512 x 512</td>
</tr>
<tr>
    <td>icon_256x256.png</td>
    <td>256 x 256</td>
</tr>
<tr>
    <td>icon_128x128@2x.png</td>
    <td>256 x 256</td>
</tr>
<tr>
    <td>icon_128x128.png</td>
    <td>128 x 128</td>
</tr>
<tr>
    <td>icon_32x32@2x.png</td>
    <td>64 x 64</td>
</tr>
<tr>
    <td>icon_32x32.png</td>
    <td>32 x 32</td>
</tr>
<tr>
    <td>icon_16x16@2x.png</td>
    <td>32 x 32</td>
</tr>
<tr>
    <td>icon_16x16.png</td>
    <td>16 x 16</td>
</tr>
</table>

Дополнительные сведения см. в документации Apple о [предоставлении версий высокого разрешения всех графических ресурсов приложения](https://developer.apple.com/library/mac/documentation/GraphicsAnimation/Conceptual/HighResolutionOSX/Optimizing/Optimizing.html#//apple_ref/doc/uid/TP40012302-CH7-SW3).


## <a name="packaging-the-icon-resources"></a>Упаковка ресурсов значка

После разработки и сохранения значка с применением требуемых размеров и имен файлов в Visual Studio для Mac можно легко назначать их ресурсам изображений для использования в Xamarin.Mac.

Выполните следующие действия:

1. На **Панели решения** откройте **Assets.xcassets** > **AppIcons.appiconset**: 

    ![Редактирование AppIcons.appiconset](app-icon-images/intro01.png "Editing the AppIcons.appiconset")
2. Для каждого необходимого размера значка щелкните значок и выберите соответствующий файл изображения, созданный выше: 

    [![Выбор изображения значка](app-icon-images/intro02.png "Selecting an icon image")](app-icon-images/intro02-large.png)
3. Сохраните изменения.


## <a name="using-the-icon"></a>Использование значка

Созданный файл `AppIcons.appiconset` необходимо назначить проекту Xamarin.Mac в Visual Studio для Mac.

Выполните следующие действия:

1. Дважды щелкните **Info.plist** на **Панели решения**, чтобы открыть окно **Параметры проекта**.
2. В разделе **Целевая платформа приложения Mac OS X** щелкните **Значки приложений**, чтобы выбрать файл `AppIcons.appiconset`: 

    [![Настройка набора значков](app-icon-images/icon01.png "Setting the icon set")](app-icon-images/icon01-large.png)
3. Сохраните изменения.

При запуске приложения на панели Dock появится новый значок:

![Пример значка приложения на панели Dock в macOS](app-icon-images/icon04.png "An example of an app icon in the macOS dock")


## <a name="summary"></a>Сводка

В этой статье описаны принципы работы с изображениями, необходимыми для создания значков приложений macOS, упаковки значков и их включения в проект Xamarin.Mac.


## <a name="related-links"></a>Связанные ссылки

- [MacImages (пример)](https://developer.xamarin.com/samples/mac/MacImages/)
- [Привет, Mac](~/mac/get-started/hello-mac.md)
- [Работа с образами](~/mac/app-fundamentals/image.md)
- [Рекомендации по работе с человеческим интерфейсом iOS. Значки и изображения](https://developer.apple.com/macos/human-interface-guidelines/icons-and-images/image-size-and-resolution/)
- [Сведения о высоком разрешении для OS X](https://developer.apple.com/library/content/documentation/GraphicsAnimation/Conceptual/HighResolutionOSX/Introduction/Introduction.html)
- [Построитель значков](https://itunes.apple.com/us/app/icns-builder/id554660130?mt=12)