---
title: Поддержка расширения Xamarin.Mac
description: В этом документе описываются в Xamarin.Mac для расширения поиска, ресурс и сегодня. Он проверяет ограничения и известные проблемы, ссылки на Пошаговое руководство и пример приложения и приводятся советы по работе с расширениями.
ms.prod: xamarin
ms.assetid: 4148F1BE-DFA0-46B6-9FCD-425A6541F510
ms.technology: xamarin-mac
author: lobrien
ms.author: laobri
ms.date: 03/14/2017
ms.openlocfilehash: 60b981a764a2656210730ae0602ff32dc580cd0a
ms.sourcegitcommit: e268fd44422d0bbc7c944a678e2cc633a0493122
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50117568"
---
# <a name="xamarinmac-extension-support"></a>Поддержка расширения Xamarin.Mac

В предварительной версии Xamarin.Mac 2.10 была добавлена поддержка нескольких точек расширения macOS:

- Служба поиска
- Общий доступ
- Сегодня

<a name="Limitations-and-Known-Issues" />

## <a name="limitations-and-known-issues"></a>Ограничения и известные проблемы

Ниже приводятся ограничения и известные проблемы, возникающие при разработке расширений в Xamarin.Mac:

* В настоящее время не поддерживается отладки в Visual Studio для Mac. Все отладки нужно будет сделать с помощью **NSLog** и **консоли**. См. в разделе советы ниже сведения.
* Расширения должны содержаться в ведущем приложении, который, будучи поочередно выполнять с регистром в системе. Которые затем должны быть включены в **расширение** раздел **системных настройках**. 
* Несколько сбоев, расширения могут дестабилизировать ведущее приложение и вызывает нестандартное поведение. В частности **Finder** и **сегодня** раздел **центр уведомлений** может стать «застревание» и перестать отвечать на запросы. Это был опыт в проектах расширений в Xcode также и вряд ли связаны с Xamarin.Mac в настоящее время отображается. Часто это можно увидеть в системном журнале (через **консоли**, Дополнительные сведения см. Советы) печати повторяющейся ошибки сообщения. Перезапуск macOS появляется, чтобы устранить эту проблему.

<a name="Tips" />

## <a name="tips"></a>Советы

Следующие советы может пригодиться при работе с расширениями в Xamarin.Mac:

- Как Xamarin.Mac в настоящее время не поддерживает расширения отладки, процесс отладки в основном зависит от выполнения и `printf` , такие как инструкции. Однако расширения выполняются в процессе "песочницы", таким образом `Console.WriteLine` не будет действовать, как и в другие приложения Xamarin.Mac. Вызов [ `NSLog` непосредственно](https://gist.github.com/chamons/e2e409013a449cfbe1f2fbe5547f6554) будет выводить сообщения отладки в системном журнале.
- Неперехваченных исключений произойдет сбой процесса расширения, обеспечивая только небольшой объем полезную информацию в **системный журнал**. Упаковки нежелательный код в `try/catch` (Exception), блокировать `NSLog`элемента перед повторным вызовом может быть полезно.
- **Системный журнал** может осуществляться из **консоли** приложение **приложений** > **служебные программы**:

    [![](extensions-images/extension02.png "Системный журнал")](extensions-images/extension02.png#lightbox)
- Как отмечалось выше, под управлением расширения ведущего приложения будет зарегистрировать в системе. Удаление пакета приложения с отменить его регистрацию. 
- Если «случайные» версии расширения приложения зарегистрированы, используйте следующую команду для их поиска (Чтобы удалить их): `plugin kit -mv`


<a name="Walkthrough-and-Sample-App" />

## <a name="walkthrough-and-sample-app"></a>Пошаговое руководство и пример приложения

Поскольку разработчик будет создавать и изменять расширения Xamarin.Mac в так же, как расширения Xamarin.iOS, обратитесь к нашей [введение расширения](~/ios/platform/extensions.md) документации для получения дополнительных сведений.

Это пример Xamarin.Mac проект, содержащий небольшой, можно найти рабочие образцы каждого типа расширения [здесь](https://developer.xamarin.com/samples/mac/ExtensionSamples/).

<a name="Summary" />

## <a name="summary"></a>Сводка

В этой статье были предприняты никакие краткий обзор работы с расширениями в приложения с подключением Xamarin.Max версии 2.10 (больше).

## <a name="related-links"></a>Связанные ссылки

- [Привет, Mac](~/mac/get-started/hello-mac.md)
- [ExtensionSamples](https://developer.xamarin.com/samples/mac/ExtensionSamples/)
- [Рекомендации по работе с человеческим интерфейсом OS X](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/OSXHIGuidelines/)
