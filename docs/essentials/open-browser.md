---
title: Xamarin.Essentials открыть браузер
description: Класс браузера в Xamarin.Essentials позволяет приложения, чтобы открыть веб-ссылку в браузере предпочтительный оптимизированного системы или внешнем браузере.
ms.assetid: BABF40CC-8BEE-43FD-BE12-6301DF27DD33
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: 7e58d439f5a6eaafe9b1b5e7ca874a986e468cb9
ms.sourcegitcommit: 51c274f37369d8965b68ff587e1c2d9865f85da7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/30/2018
ms.locfileid: "39353286"
---
# <a name="xamarinessentials-browser"></a>Xamarin.Essentials: браузера

![Предварительные версии NuGet](~/media/shared/pre-release.png)

**Браузера** класс позволяет приложения, чтобы открыть веб-ссылку в браузере предпочтительный оптимизированного системы или внешнем браузере.

## <a name="using-browser"></a>С помощью браузера

Добавьте ссылку на Xamarin.Essentials в классе:

```csharp
using Xamarin.Essentials;
```

Функциональность обозревателя работает путем вызова `OpenAsync` метод с `Uri` и `BrowserLaunchMode`.

```csharp

public class BrowserTest
{
    public async Task OpenBrowser(Uri uri)
    {
        await Browser.OpenAsync(uri, BrowserLaunchMode.SystemPreferred);
    }
}
```

## <a name="platform-implementation-specifics"></a>Особенности реализации платформы

# <a name="androidtabandroid"></a>[Android](#tab/android)

Режим запуска определяет, как будет запущен браузер:

## <a name="system-preferred"></a>Предпочитаемый системы

[Chrome настраиваемые вкладки](https://developer.chrome.com/multidevice/android/customtabs) будет предпринята попытка использовать Uri загрузить и сохранить осведомленности в области навигации.

## <a name="external"></a>Внешняя

`Intent` Будет использоваться для запроса Uri будет открыт с помощью обычного браузера системы.

# <a name="iostabios"></a>[iOS](#tab/ios)

## <a name="system-preferred"></a>Предпочитаемый системы

[SFSafariViewController](https://developer.xamarin.com/api/type/SafariServices.SFSafariViewController/) до используется для загрузки Uri и сохранить осведомленности в области навигации.

## <a name="external"></a>Внешняя

Стандартный `OpenUrl` на основного приложения используется для запуска браузера по умолчанию вне приложения.

# <a name="uwptabuwp"></a>[UWP](#tab/uwp)

Всегда будет запущен браузер пользователя по умолчанию вне зависимости от `BrowserLaunchMode`.

--------------

## <a name="api"></a>API

- [Обозреватель исходного кода](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Browser)
- [Документация по API браузера](xref:Xamarin.Essentials.Browser)
