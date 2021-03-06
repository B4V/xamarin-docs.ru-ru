---
title: Изображения и значки в Xamarin.iOS
description: Этот раздел содержит множество статей, расскажем о работе с изображениями в приложение Xamarin.iOS, например, использование их в виде значков, запуска экранов и включая их в элементы управления и значки для типов пользовательских документов.
ms.prod: xamarin
ms.assetid: 0AB8CC07-11E4-0D75-4119-AED1A1252424
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 03/18/2017
ms.openlocfilehash: 09afcac8dcecd5a1d05961c2981c0940fff00a01
ms.sourcegitcommit: e268fd44422d0bbc7c944a678e2cc633a0493122
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50102364"
---
# <a name="images-and-icons-in-xamarinios"></a>Изображения и значки в Xamarin.iOS

_Этот раздел содержит множество статей, расскажем о работе с изображениями в приложение Xamarin.iOS, например, использование их в виде значков, запуска экранов и включая их в элементы управления и значки для типов пользовательских документов._

Существует несколько способов этого образа, ресурсы, используемые в приложении iOS. Просто отображать изображения как часть пользовательского интерфейса приложения, назначив ей к элементу управления пользовательского интерфейса, такие как `UIButton` или `UIImageView`, для предоставления значков и экранов запуска, Xamarin.iOS упрощает добавление полезные иллюстрации в приложение iOS, одним из следующих способов: 

- **Независимые изображения с разрешением** — использовать встроенную поддержку в iOS для работы с изображениями в разрешениях различных устройств и типов (iPhone, iPad, и т.д.).
- **Наборы изображений каталога активов** -использование **наборы изображений каталога активов** для управления и сгруппировать все версию ресурса заданного изображения, необходимые приложения.
- **Образы в конструкторе iOS** -использовать конструктор iOS для установки образов для элементов управления.
- **Образы в коде** — использование `UIImage` методы класса для загрузки и работы с ресурсами, изображение и назначить их к элементам управления пользовательского интерфейса в C# кода.
- **Значок приложения** -определение требующегося каждое приложение iOS значка приложения. Это значок, который пользователь сможет нажать с начального экрана iOS для запуска приложения. Кроме того этот значок используется Game Center, если применимо.
- **Spotlight значок** -определить Spotlight значка приложения. Всякий раз, когда пользователь вводит имя приложения в поиске Spotlight, отображается этот значок.
- **Значок "Параметры"** — определить приложения **параметры** значок. Если пользователь введет **параметры** приложение на своем устройстве iOS, этот значок будет отображаться в конце списка параметров для приложения. 
- **Экраны запуска** -определение экрана запуска приложения. При касании значка приложения и до появления первое представление, будет отображаться пустой экран. К счастью в iOS включает поддержку для отображения изображения вместо пустой экран с помощью раскадровки. 
- **Значок iTunes** -представляет значок iTune. При использовании метода Ad-Hoc доставки приложения (либо для корпоративных пользователей, либо для бета-тестирование на реальных устройствах), разработчик также необходимо включить 512 x 512 и 1024 x 1024 образ, который будет использоваться для представления приложения в iTunes.
- **Документирование значки** -использовать изображение в качестве значка для любого типа определенного документа, который поддерживает приложения Xamarin.iOS, или создает.

Существует несколько факторов, которые следует принимать во внимание при создании графические активы для приложения iOS, а также нескольких местах, где будут использоваться эти ресурсы. Каждый из этих оказывать влияние на не только графические активы, сколько потребуется, но создание этих ресурсов. Типы ресурсов изображений, которые будут необходимы, как эти средства включены в пакет приложения и как используются ресурсы изображений для выбранных функций рассматриваются в следующих разделах:


## <a name="displaying-an-imageiosapp-fundamentalsimages-iconsdisplaying-an-imagemd"></a>[Отображение изображения](~/ios/app-fundamentals/images-icons/displaying-an-image.md)

В этой статье рассматриваются включая ресурс изображения в приложение Xamarin.iOS и отображение этого образа, либо с помощью кода C#, либо, присвоив его к элементу управления в конструкторе iOS.

## <a name="application-iconsiosapp-fundamentalsimages-iconsapp-iconsmd"></a>[Значки приложения](~/ios/app-fundamentals/images-icons/app-icons.md)

Этот статье охватывает, включая и управление ими ресурс изображения в приложение Xamarin.iOS для использования в качестве значка приложения.

## <a name="alternate-app-iconsiosapp-fundamentalsimages-iconsalternate-app-iconsmd"></a>[Альтернативные значки приложений](~/ios/app-fundamentals/images-icons/alternate-app-icons.md)

Apple добавлено несколько улучшений iOS 10.3, разрешить приложение для управления его значок:

 - `ApplicationIconBadgeNumber` — Получает или задает эмблему на значок приложения в Springboard.
 - `SupportsAlternateIcons` Если `true` приложение имеет дополнительный набор значков.
 - `AlternateIconName` — Возвращает имя выбранного альтернативный значок или `null` при использовании основной значок.
 - `SetAlternameIconName` -Используйте этот метод переключиться на альтернативный значок заданного значка приложения.


## <a name="launch-screensiosapp-fundamentalsimages-iconslaunch-screensmd"></a>[Экраны запуска](~/ios/app-fundamentals/images-icons/launch-screens.md)

Этой статье описывается использование специальный тип раскадровки для обеспечения универсальной экран запуска для каждой iOS размера и разрешения устройства.

## <a name="custom-document-typesiosapp-fundamentalsimages-iconscustom-document-typesmd"></a>[Типы настраиваемых документов](~/ios/app-fundamentals/images-icons/custom-document-types.md)

Этот статье охватывает, включая и управление ими ресурс изображения в приложение Xamarin.iOS для использования в качестве пользовательский значок типа документа.



## <a name="related-links"></a>Связанные ссылки

- [Работа с образами (пример)](https://developer.xamarin.com/samples/WorkingWithImages/)
- [Hello, iPhone](~/ios/get-started/hello-ios/index.md)
- [Пользовательский значок и правила создания образа](http://developer.apple.com/library/ios/#documentation/UserExperience/Conceptual/MobileHIG/IconsImages/IconsImages.html)
