---
title: API-интерфейсы поиска в Xamarin.iOS
description: В этой статье описывается с помощью новых интерфейсов API поиска приложений в iOS 9, чтобы разрешить пользователям искать сведения и функции внутри приложений Xamarin.iOS.
ms.prod: xamarin
ms.assetid: 7323EB3D-A78F-4BF0-9990-3160C7E83CF0
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 03/20/2017
ms.openlocfilehash: 799d6dd532e530f5ee9c9a974b2d93b6a3be0efb
ms.sourcegitcommit: e268fd44422d0bbc7c944a678e2cc633a0493122
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50122417"
---
# <a name="search-apis-in-xamarinios"></a>API-интерфейсы поиска в Xamarin.iOS

_В этой статье описывается с помощью интерфейсов API поиска приложений в iOS 9, чтобы разрешить пользователям искать сведения и функции внутри приложений Xamarin.iOS._

Поиск была расширена в iOS 9, чтобы предоставить новые способы доступа к данным и функциям в приложении Xamarin.iOS. С помощью новых интерфейсов API поиска приложений, содержимое приложения становится доступным для поиска в центре внимания и Safari результатах поиска, передачи и напоминания Siri и предложения. Это позволяет быстро получить доступ к действий и сведений, глубоко внутри приложения.

Кроме того новые API-интерфейсы поиска облегчают интегрировать систему поиска в приложении без опыта реализации предыдущего поиска. По этой причине Apple заявляет, что обычно занимает несколько часов, чтобы обеспечить универсально для поиска с помощью приложения поиска содержимого с приложением iOS 9.

[![](images/intro01.png "Пример содержимого приложения iOS 9, глобально доступные для поиска с помощью приложения поиска")](images/intro01.png#lightbox)

Приложение поиска состоит из трех независимых API:

1. [**NSUserActivity** ](nsuseractivity.md) -это расширение переадресации API, которые Apple выпущена в iOS 8. Он используется, чтобы сделать журнал взаимодействия приложения с возможностью поиска как в открытых, так и в частном порядке) пользователем.

2. [**Основы Spotlight** ](corespotlight.md) -позволяет приложению для индексирования его содержимого, должна присутствовать в результатах поиска. Он работает подобно API, где элементы могут быть добавлены и удалены, и это лучший способ индекс конфиденциальное содержимое в приложении базы данных.

3. [**WebMarkup** ](web-markup.md) — для приложений, которые предоставляют доступ к своему содержимому через веб-интерфейс (не только в приложении). Веб-содержимого можно пометить специальные ссылки, которые компанией Apple для обхода и обеспечивают создание глубинных ссылок в приложение на устройствах пользователей iOS 9.

## <a name="selecting-an-app-search-approach"></a>Выбор подхода приложения поиска

Решить, какие из этих методов для реализации зависит от типов взаимодействия, предоставляемые приложения и тип содержимого, которые она представляет.

Следуйте приведенным ниже рекомендациям:

- [**NSUserActivity** ](nsuseractivity.md) — использовать эту инфраструктуру для обеспечения возможности поиска и общедоступных и частных содержимое и также возможность поиска точек навигации в приложении.

- [**Основы Spotlight** ](corespotlight.md) — использовать эту инфраструктуру для обеспечения возможности поиска личных данных, хранящихся на устройстве.

- [**Веб-разметка** ](web-markup.md) — использовать эту инфраструктуру для обеспечения возможности поиска для приложений, которые предлагают содержимое не только от в приложении, но с веб-сайта приложения также.

Каждый из поиска приложения подходы отличаются и может быть использовать по отдельности, однако Apple, спроектировали эти устройства для совместной работы. При использовании более чем одним из подходов к индекс конкретного элемента, убедитесь, что используется же **идентификатор элемента** на каждый подход, таким образом, он связывает работы.

С помощью более чем одним из подходов не только гарантирует, что содержимое будет найден конечным пользователем, но также позволяет повысить рейтинг вашего элемента из в службе поиска.

Во время процесса ранжирования в основном прозрачно для разработчика, взаимодействие пользователя с указанным элементом, рассматривает сильно при этом ранг (например пользователя, нажмите ссылку).
Предоставляя подробные и информативные элементы, гарантирует, что пользователь будет запустит для взаимодействия с содержимого, таким образом, вызов ранжирование.

## <a name="what-content-to-index"></a>Материал для индекса

Компания Apple предоставляет следующие советы о том, какое содержимое и действия для предоставления индексы поиска для приложения:

 - Любое содержимое, просматривать, создавать или курирует пользователям в приложении.
 - Точки навигации и функции в приложении.
 - Такие вещи, как новые сообщения, содержимое или другие виды элементов, отображаемых на приложения, которые недавно были загружены на устройство.

## <a name="app-search-enhancements"></a>Улучшенные возможности поиска приложения

Полезные сведения в iOS 10 содержит ряд усовершенствований для поиска приложения:

- **Популярность приобщиться прямой ссылкой (с разностной конфиденциальности)** -предоставляет способ распространения содержимого прямая ссылка на приложение в результатах поиска.
- **Поиск в приложении** -использовать новый `CSSearchQuery` класс обеспечивает возможность поиска Spotlight в приложении аналогичную как работают приложения почта, сообщения и заметки.
- **Поиск продолжения** — пользователь может начать поиск в центре внимания или Safari, а затем откройте приложение и по-прежнему поиска.
- **Визуализация результатов проверки** -Apple [средство проверки API поиска приложения](https://search.developer.apple.com/appsearch-validation-tool) теперь отображает визуальное представление разметки веб сайта и связывание глубокого preforming тестов.
- **Сообщения, общий доступ к приложениям образ** -позволяет популярных изображений в приложении для отображаться в результатах поиска Spotlight совместного использования в сообщениях (через расширение приложения сообщения).

Чтобы узнать больше, ознакомьтесь с разделом наших [улучшенные возможности поиска приложения](~/ios/platform/search/app-search-enhancements.md) руководства.

### <a name="proactive-suggestions"></a>Упреждающие предложения

iOS 10 предоставляет новые способы вождения взаимодействия в приложение, позволив системе, чтобы заранее предоставить полезные сведения автоматически пользователю в нужное время. Так же, как iOS 9 предоставлена возможность добавления комплексный поиск в приложение с помощью Spotlight, Эстафетной и предложения Siri с iOS 10, приложение может предоставлять функциональные возможности, могут быть представлены пользователю системой из в следующих расположениях:

- Переключатель приложения
- На экране блокировки
- CarPlay
- Карты
- Siri взаимодействия
- QuickType предложения 

Приложение поддерживает эту функцию в систему с помощью набора технологий, таких как [NSUserActivity](https://developer.xamarin.com/api/type/Foundation.NSUserActivity/), веб-разметка, полезные сведения, MapKit, проигрыватель мультимедиа и UIKit.

Чтобы узнать больше, ознакомьтесь с разделом наших [упреждающие предложения](~/ios/platform/search/proactive-suggestions.md) руководства.

## <a name="summary"></a>Сводка

В этой статье подробно рассматривается новой функции API-Интерфейсов поиска, iOS 9 предоставляет для приложений Xamarin.iOS. Его обеспечить [NSUserActivity](nsuseractivity.md), [полезные сведения](corespotlight.md) и [веб-разметка](web-markup.md) методы для индексирования содержимого. Оно завершено с краткое обсуждение, когда следует использовать подход поиска и типы содержимого, которые должны быть проиндексированы.



## <a name="related-links"></a>Связанные ссылки

- [Примеры iOS 9](https://developer.xamarin.com/samples/ios/iOS9/)
- [iOS 9 для разработчиков](https://developer.apple.com/ios/pre-release/)
- [iOS 9.0](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html)
- [Руководство по программированию приложения поиска](https://developer.apple.com/library/prerelease/ios/documentation/General/Conceptual/AppSearch/index.html#//apple_ref/doc/uid/TP40016308)
