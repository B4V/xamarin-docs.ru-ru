---
title: Совместное использование кода на нескольких платформах
description: Этот документ содержит ссылки на различные руководства, описывающие способы совместного использования кода, включая переносимые библиотеки классов, общие проекты, .NET Standard и NuGet.
ms.prod: xamarin
ms.assetid: 7D179ACF-09A6-46EE-B49D-E27AB5F09CD4
author: conceptdev
ms.author: crdun
ms.date: 07/18/2018
ms.openlocfilehash: 3a2c3f98e3ba83db0794a68ff1d62a9845a111c0
ms.sourcegitcommit: 46bb04016d3c35d91ff434b38474e0cb8197961b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/26/2018
ms.locfileid: "39270193"
---
# <a name="sharing-code-on-multiple-platforms"></a>Совместное использование кода на нескольких платформах

В этой статье рассматривается различные параметры, доступные для совместного использования кода на платформах, включая Windows, Android, iOS и многое другое.

## <a name="code-sharing-overviewcode-sharingmd"></a>[Совместное использование Обзор кода](code-sharing.md)

Дополнительные сведения о различных параметры, доступные для проектов Xamarin, включая стандартные библиотеки .NET и проектах общих совместного использования кода. Переносимые библиотеки классов, также поддерживаются, однако считается устаревшим в связи с .NET Standard.

## <a name="net-standardcross-platformapp-fundamentalsnet-standardmd"></a>[.NET Standard](~/cross-platform/app-fundamentals/net-standard.md)

.NET standard является предпочтительным при совместное использование кода несколькими платформами. Код создан для конкретной версии (2.0 обеспечивает лучший API совместимости с существующим кодом .NET Framework) и может быть принято элементом других проектов, которые поддерживают этот уровень или более поздней версии. Проектов .NET standard, поддерживаются в Visual Studio 2017 и Visual Studio для Mac.

## <a name="shared-projectscross-platformapp-fundamentalsshared-projectsmd"></a>[Общие проекты](~/cross-platform/app-fundamentals/shared-projects.md)

Общие проекты позволяют писать общий код, на который ссылается несколько проектов различных приложений. Код компилируется как часть каждого ссылающийся проект и могут включать директивы компилятора для внедрения функциональных возможностей платформы базы общего кода. В этой статье рассматриваются как общие проекты работают и как создать и использовать их с проектами Xamarin.

## <a name="portable-class-librariescross-platformapp-fundamentalspclmd"></a>[Переносимые библиотеки классов](~/cross-platform/app-fundamentals/pcl.md)

Проекты переносимой библиотеки классов можно создавать и распространять сборки, содержащие общий код для запуска на нескольких платформах. Для создания переносимой библиотеки классов (или «PCL») сначала выбрать какие платформы для целевой, а затем написать код для подмножество .NET Framework, которая доступна в профиле, определенных для этих платформ. PCL считается устаревшим в последних версиях Visual Studio; Разработчики, рекомендуется вместо этого использовать .NET Standard 2.0.

## <a name="nuget-projects-multiplatform-libraries-for-code-sharingcross-platformapp-fundamentalsnuget-multiplatform-librariesindexmd"></a>[Проекты NuGet: многоплатформенного библиотек для совместного использования кода](~/cross-platform/app-fundamentals/nuget-multiplatform-libraries/index.md)

Пакеты NuGet можно автоматически создавать из проектов переносимой библиотеки Классов или .NET standard; и проектах общих можно упаковать в пакеты NuGet «с подменой», с помощью отдельный тип проекта NuGet. В этом разделе описывается создание пакетов NuGet для каждого сценария совместного использования кода.

## <a name="manually-creating-nuget-packages-for-xamarincross-platformapp-fundamentalsnuget-manualmd"></a>[Вручную созданию пакетов NuGet для Xamarin](~/cross-platform/app-fundamentals/nuget-manual.md)

Советы по созданию пакетов NuGet, которые работают на платформе Xamarin.
