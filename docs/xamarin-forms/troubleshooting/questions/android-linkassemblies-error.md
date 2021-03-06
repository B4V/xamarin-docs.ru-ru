---
title: Ошибка сборки Android — непредвиденный сбой задачи LinkAssemblies
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: EB3BE685-CB72-48E3-89D7-C845E76B9FA2
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/25/2017
ms.openlocfilehash: 7360ee9064049bcebfd88f0cd36b5938d5337be3
ms.sourcegitcommit: e268fd44422d0bbc7c944a678e2cc633a0493122
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50105289"
---
# <a name="android-build-error--the-linkassemblies-task-failed-unexpectedly"></a>Ошибка сборки Android — непредвиденный сбой задачи LinkAssemblies

Может появиться сообщение об ошибке `The "LinkAssemblies" task failed unexpectedly` при построении проекта Xamarin.Android, в котором используются форм. Это происходит, когда компоновщик активен (обычно при *выпуска* сборки, чтобы уменьшить размер пакета приложения); и она выполняется, так как Android целевые объекты не обновлен до последней версии framework. (Дополнительные сведения: [Xamarin.Forms для Android требования](~/xamarin-forms/get-started/installation.md#android))

Решение этой проблемы является обеспечение того, можно иметь последнюю поддерживаемую версию пакета SDK для Android и задать **требуемой версии .NET Framework** для **использовать самую новую установленную платформу**. Кроме того, рекомендуется установить **целевая версия Android** для **использовать версию целевой платформы** и **Минимальная версия Android** API 15 или более поздней версии. Это считается поддерживаемой конфигурации.

## <a name="setting-in-visual-studio-for-mac"></a>Настройки в Visual Studio для Mac

1.  Щелкните правой кнопкой мыши проект Android.
2.  Перейдите к **сборки > Общие > платформы**.
3.  Задайте **требуемой версии .NET Framework: использовать самую новую установленную платформу**.
4.  По-прежнему в параметры проекта, перейдите в раздел **сборки > приложение Android**.
5.  Задайте **минимум Android версии** для API уровня 15 или более поздней версии & **целевая версия Android** для **автоматически — использовать версию целевой платформы**.

## <a name="setting-in-visual-studio"></a>В Visual Studio

1.  Щелкните правой кнопкой мыши проект Android.
2.  Перейдите к **приложения** в параметрах проекта.
3.  Задайте **компиляции с помощью версии Android** & **целевая версия Android** параметры, чтобы **использовать последнюю платформу** / **использования Компиляция с помощью пакета SDK версии**.
4.  Задайте **минимум Android к целевому объекту** параметр API 19 или выше.

После обновления этих параметров, очистка и заново Постройте свой проект, чтобы убедиться, что ваши изменения будут применены.
